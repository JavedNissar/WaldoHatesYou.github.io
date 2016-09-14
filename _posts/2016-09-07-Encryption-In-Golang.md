---
layout: post
---
When I dove into the world of encryption in the Go programming language. The
general recommendation I discovered was that I should use a Go port of the
popular cryptography library Nacl. That being said, I did have issues using it
in the beginning as I found the documentation to be lacking in examples. So,
in this post I will illustrate the use of the Nacl cryptography library in Go.
{%highlight Go %}
import(
  "log"
  "golang.org/x/crypto/pbkdf2"
	"golang.org/x/crypto/nacl/secretbox"
  "crypto/sha1"
)

/*The following is an encryption function in Golang using Nacl and PBDKF2
This encryption function takes data as a string,a slice of bytes for the salt,
and a string for the password as well*/
func Encrypt(data string,salt []byte,password string) ([]byte){
  /*
  The following line generates the encryption key. This key is important because
  it is what you will need to encrypt and decrypt the data. PBDKF2 is used
  because it is what NIST recommends for this usecase. Keep in mind that the
  number of iterations must be above 1000. Furthermore, the keySize should be
  large (e.g it can't be 4). This example uses a key-size of 32. The hash
  function used in this one is SHA1 but in general, SHA-2 is better.
  */
  generatedKey := pbkdf2.Key([]byte (password),salt,iterations,keySize,sha1.New)

  /*
  The following line generates a nonce and the nonce is some bytes that are
  used to ensure that if you have the same data, the encrypted data will
  be different each time. Keep in mind that the nonce should only be used once.
  */
  generatedNonce,nonceErr := GenerateRandomBytes(nonceSize)

  /*
  The following line initializes an array to hold the nonce. This is because
  Nacl doesn't take slices.
  */
  nonce := new([24]byte)

  /*
  copy the generated nonce to the array
  */
  copy(nonce[:],generatedNonce[:nonceSize])

  //init a var to hold the key for the same purpose as the nonce
  key := new([keySize]byte)

  /*
  copy the generated key to an array
  */
  copy(key[:],generatedKey[:keySize])

  //Log the error if present
  if nonceErr != nil{
    log.Fatal(nonceErr)
  }

  /*
  initialize an array for the encrypted data
  */
  encryptedData := make([]byte, nonceSize)
  /*
  Copy the nonce over to the encrypted data. The idea behind this is that
  */
  copy(encryptedData, nonce[:])
  /*
  Complete the encryption process
  */
  encryptedData = secretbox.Seal(encryptedData, []byte (data), nonce, key)

  return encryptedData
}

func Decrypt(encryptedData []byte,salt []byte, password string) ([]byte, error){
	/*
  The following line is used to regenerate the encryption key from the encryption
  process. It is imperative that the salt and password used to encrypt are
  provided again.
  */
	generatedKey := pbkdf2.Key([]byte (password),salt,iterations,keySize,sha1.New)

  /*
  Set up variables to hold the key
  */
	key := new([keySize]byte)
	//this step is necessary to convert generatedKey to a var of type [32]byte
	//[32]byte is the type that Nacl requires for encryption
  /*
  copy the key to an array like last time
  */
	copy(key[:], generatedKey[:keySize])

	//set up a var to hold the nonce
	nonce := new([nonceSize]byte)

	/*
  Copy the nonce which is currently hidden inside encryptedData into nonce.
  Keep in mind that the nonce does not have to be part of the encrypted data.
  It could instead be placed away from the encrypted data if you feel like that
  is necessary for your usecase.
  */
	copy(nonce[:], encryptedData[:nonceSize])

	//decrypt the data using everything from earlier
	data, decryptionSuccess := secretbox.Open(nil, encryptedData[nonceSize:], nonce, key)

	if decryptionSuccess{
		return data,nil
	}else{
		return nil,errors.New("Decryption failed")
	}
}
{% endhighlight %}
