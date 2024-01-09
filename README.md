# SecureDataManager Library

The `SecureDataManager` library is designed to provide secure encryption and storage of sensitive information in Android applications. It utilizes the AndroidKeyStore for key management and follows best practices for secure data handling.

## Encryption Algorithm

The library employs the Advanced Encryption Standard (AES) algorithm with Cipher Block Chaining (CBC) mode and PKCS7 padding. The transformation used is `AES/CBC/PKCS7Padding`.

## Installation

To integrate the SecureDataManager library into your Android project, follow these steps:

1. Add the library as a dependency in your app's `build.gradle` file:

   ```gradle
   implementation project(":securestorage")
   ```


## Usage

### Initialization

To use the SecureDataManager in your Android application, first, initialize it in your activity or application class:

```kotlin
val secureDataManager = SecureDataManager()
```

### Encrypting Data

Encrypt sensitive data using the `encrypt` method:

```kotlin
val dataToEncrypt = "Sensitive information".toByteArray()
val encryptedData = secureDataManager.encrypt(dataToEncrypt)
```

### Decrypting Data

Decrypt previously encrypted data using the `decrypt` method:

```kotlin
val decryptedData = secureDataManager.decrypt(encryptedData)
```

### Example in MainActivity

The following is an example of how to use SecureDataManager in your MainActivity:

```kotlin
class MainActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // Initialize SecureDataManager
        val secureDataManager = SecureDataManager()

        // Encrypt data
        val bytes = messageToEncrypt.encodeToByteArray()

        // Store the encrypted data in a file
        val file = File(filesDir, "secret.txt")
        if (!file.exists()) {
            file.createNewFile()
        }
        val fos = FileOutputStream(file)
        val encryptedData = secureDataManager.encrypt(bytes)
        fos.write(encryptedData)
        fos.close()

        // Decrypt data
        val data = FileInputStream(file).readBytes()
        messageDecrypted = secureDataManager.decrypt(data)

    }
}

```
In this example, the encrypted data is stored in a file named "secret.txt" using a FileOutputStream. Later, when decrypting, the data is read from the same file using a FileInputStream. Make sure to adjust the file name and path according to your project's requirements.

## Security Considerations

The library utilizes the AndroidKeyStore for secure key storage, providing an additional layer of protection for sensitive data.
