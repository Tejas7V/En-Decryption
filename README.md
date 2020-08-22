//Function for en/decryption
private static final String ALGORITHM = "AES";
private static final String TRANSFORMATION = "AES";
 
    public static String encrypt(String key, String inputStr)
            throws CryptoException {
        return doCrypto(Cipher.ENCRYPT_MODE, key, inputStr);
    }
 
    public static String decrypt(String key, String inputStr)
            throws CryptoException {
        return doCrypto(Cipher.DECRYPT_MODE, key, inputStr);
    }
 
    private static String doCrypto(int cipherMode, String key, String inputStr) throws CryptoException {
        try {
            Key secretKey = new SecretKeySpec(key.getBytes(), ALGORITHM);
            Cipher cipher = Cipher.getInstance(TRANSFORMATION);
            cipher.init(cipherMode, secretKey);
            
            byte[] inputBytes = inputStr.GetBytes();
             
            byte[] outputBytes = cipher.doFinal(inputBytes);
             
            return new String(outputBytes);
             
        } catch (NoSuchPaddingException | NoSuchAlgorithmException
                | InvalidKeyException | BadPaddingException
                | IllegalBlockSizeException | IOException ex) {
            throw new CryptoException("Error encrypting/decrypting string", ex);
        }
    }
