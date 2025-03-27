# Bajaj_Code

import org.json.JSONObject;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.security.MessageDigest;

import java.nio.file.Files;
import java.nio.file.Paths;
import java.security.MessageDigest;

public class JsonParser {

    private static final String INPUT_FILE = "input.json";
    private static final String OUTPUT_FILE = "output.txt";

    public static void main(String[] args) {
        try {
            // Read the JSON file
            System.out.println("Reading JSON file...");
            String content = new String(Files.readAllBytes(Paths.get(INPUT_FILE)));
            System.out.println("JSON content: " + content);

            System.out.println("JSON content: " + content);

            JSONObject jsonObject = new JSONObject(content);

            // Extract first_name and roll_number
            String firstName = jsonObject.getJSONObject("student").getString("first_name").toLowerCase();
            String rollNumber = jsonObject.getJSONObject("student").getString("roll_number").toLowerCase();
            System.out.println("Extracted first_name: " + firstName);
            System.out.println("Extracted roll_number: " + rollNumber);

            System.out.println("Extracted first_name: " + firstName);
            System.out.println("Extracted roll_number: " + rollNumber);

            // Concatenate and generate MD5 hash
            String concatenated = firstName + rollNumber;
            String md5Hash = generateMD5(concatenated);
            System.out.println("Generated MD5 Hash: " + md5Hash);

            // Write the output to output.txt
            Files.write(Paths.get(OUTPUT_FILE), md5Hash.getBytes());
            System.out.println("MD5 Hash written to " + OUTPUT_FILE);

            System.out.println("MD5 Hash written to " + OUTPUT_FILE);
        } catch (Exception e) {
            System.err.println("Error: " + e.getMessage());
            e.printStackTrace();
        }
    }

    private static String generateMD5(String input) throws Exception {
        MessageDigest md = MessageDigest.getInstance("MD5");
        byte[] messageDigest = md.digest(input.getBytes());
        StringBuilder hexString = new StringBuilder();
        for (byte b : messageDigest) {
            String hex = Integer.toHexString(0xff & b);
            if (hex.length() == 1) hexString.append('0');
            hexString.append(hex);
        }
        return hexString.toString();
    }
}
