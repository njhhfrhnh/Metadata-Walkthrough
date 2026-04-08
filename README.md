# Metadata Analysis Walkthrough

This repository contains a walkthrough for Metadata analysis and hidden data extraction techniques from image files.

The objective of this lab is to understand how hidden information can be stored inside files and how to extract it using different forensic tools.

---

## Tools Used
- exiftool
- hexeditor
- binwalk
- strings
- file

---

## Walkthrough

### 1. Exiftool (Metadata Analysis)

Command:
exiftool ocean.jpg

- Purpose: To extract metadata from an image file
- Explanation: Metadata contains hidden information such as file details, timestamps, and embedded data that cannot be seen normally
- Result: A hidden comment was found in the metadata

This shows that images can store hidden information inside metadata fields such as comments.

---

### 2. Hexeditor (Raw File Analysis)

Command:
hexeditor computer.jpg

- Purpose: To view the raw binary content of the file
- Explanation: Displays both hexadecimal values and ASCII-readable text
- Observation:
  - Left side → hexadecimal values
  - Right side → readable text

- Result: No hidden flag was found after analyzing the content

This indicates that the file only contains normal data without embedded hidden messages.

---

### 3. Binwalk (Hidden File Detection)

Command 1:
binwalk dog.jpg

- Purpose: To scan for hidden or embedded files inside the image
- Result:
  - Detected a ZIP archive inside the image
  - Found at offset 88221
  - File identified: hidden_text.txt

Command 2:
binwalk -e dog.jpg

- Purpose: To automatically extract hidden files
- Result: Extraction failed with warning

This means the file was detected but required manual extraction.

---

### 4. Manual Extraction (dd + unzip)

Command:
dd if=dog.jpg of=hidden.zip bs=1 skip=88221

- Purpose: To manually extract the hidden ZIP file using the offset value
- Explanation:
  - if → input file
  - of → output file
  - bs=1 → copy byte by byte
  - skip → start extracting from specific offset

Command:
unzip hidden.zip

- Purpose: Extract contents of ZIP file
- Result: hidden_text.txt successfully extracted

Command:
cat hidden_text.txt

- Purpose: Display file content
- Result: Hidden message found

This confirms that files can be embedded inside images and require manual extraction techniques.

---

### 5. Strings (Readable Text Extraction)

Command:
strings computer.jpg

- Purpose: To extract human-readable text from binary files
- Result:
  - Found common strings such as:
    - JFIF
    - ICC_PROFILE
    - RGB XYZ
    - lcms

- Conclusion: No hidden flag found

This shows that not all files contain hidden data, even if readable strings are present.

---

### 6. File Command (File Type Verification)

Command:
file solitaire.exe

- Purpose: To identify the real file type based on content
- Result: File is actually a PNG image, not an executable

Command:
file rubiks.jpg

- Purpose: Verify file format
- Result: File is PNG format even though extension is .jpg

This demonstrates that file extensions can be misleading and should not be trusted blindly.

---

## Conclusion

This lab demonstrates:
- Metadata analysis using Exiftool
- Binary inspection using Hexeditor
- Hidden file detection using Binwalk
- Manual extraction using dd and unzip
- Text extraction using strings
- File type verification using file command

Overall, it highlights how attackers can hide data inside files and how forensic tools can be used to uncover them.

---

## File Included
- METADATA WALKTHROUGH W4 LAB.pdf

---

## ⚠️ Disclaimer
This walkthrough is for educational purposes only. All activities were conducted in a controlled lab environment.
