# Upload Body Composition Data to Garmin Connect

This guide provides a simple, free method to upload full body composition data (weight, body fat, BMI, muscle mass, etc.) from any scale that supports CSV export (like Renpho) into Garmin Connect.

This process avoids the need to buy the expensive Garmin Index S2 scale. It uses Garmin's own official FIT SDK tools to convert a CSV file into a `.fit` file that Garmin Connect can import.

This work is an expansion of the foundational guide created by [SAShood on Reddit](https://www.reddit.com/r/Garmin/comments/18t8fq5/omron_body_composition_to_garmin_connect/).

## Features
* **Free:** Does not require any paid software.
* **Official Tools:** Uses Garmin's official `FitCSVTool.jar`.
* **No Coding Required:** Just copying/pasting in a spreadsheet and running one command.
* **Comprehensive Data:** Imports not just weight, but also:
    * Body Fat %
    * Body Water %
    * BMI
    * Muscle Mass
    * Visceral Fat

## The 3-Step Process
1.  **Prep Your Data:** Use the Google Sheet Template to format your scale's CSV data.
2.  **Get Garmin's Tool:** Download the official FIT SDK to get `FitCSVTool.jar`.
3.  **Convert & Upload:** Run one command to create your `.fit` file and upload it to Garmin Connect.

---

## Detailed Step-by-Step Instructions

### Step 1: Get the Google Sheet Template
1.  Go to the [Google Sheet Template](https://docs.google.com/spreadsheets/d/1M4Asm_EOTkRxYQg7qDRoLPaaXiEMKlDFAjEIp6G5tJg/edit?usp=sharing).
2.  Click **File > Make a copy** to save it to your own Google Drive.
3.  (Alternatively, you can download the `garmin_sdk_ready_template.csv` from this repo and edit it locally.)

### Step 2: Add Your Data
1.  Open the **"Your_Data_Import"** sheet (the 2nd tab).
2.  Export your data from your scale's app (e.g., Renpho) and paste it into this sheet.
3.  **Crucial:** The "Garmin Timestamp" column (Column A) has a formula to convert your date/time. Make sure to copy this formula down for all your rows. (formula if you downloaded the local file: =INT((VALUE(SUBSTITUTE(SUBSTITUTE(A2, " at ", " "), CHAR(8239), " ")) - 32874) * 86400))

### Step 3: Prepare the Garmin Template
1.  Click on the **"GARMIN_CSV_TEMPLATE"** sheet (the 1st tab).
2.  Copy and paste your data from the "Your_Data_Import" sheet into the correct columns. The sheet is set up to make this easy.
3.  **Do not change** the first two rows (the "Type" and "Definition" headers).
4.  Drag your data rows down to match the number of entries you have.

### Step 4: Download the SDK and CSV
1.  From your Google Sheet, click **File > Download > Comma Separated Values (.csv)**.
2.  Save the file with the exact name: `garmin_sdk_ready.csv`.
3.  Go to the [Garmin FIT SDK page](https://developer.garmin.com/fit/download/) and download the SDK.
4.  Unzip the SDK, open the `java` folder, and find the file `FitCSVTool.jar`.
5.  **Important:** Create a new, empty folder (e.g., on your Desktop) and copy both `garmin_sdk_ready.csv` and `FitCSVTool.jar` into this same folder.

### Step 5: Run the Conversion
1.  Open your terminal or command prompt.
2.  Use the `cd` command to navigate into the folder you just created.
    * *Example for Mac:* `cd ~/Desktop/GarminUpload`
    * *Example for Windows:* `cd C:\Users\YourName\Desktop\GarminUpload`
3.  Run the following command (it's the same for Mac and Windows):
    ```bash
    java -jar FitCSVTool.jar -c garmin_sdk_ready.csv my_body_data.fit
    ```
    *(Note: This requires you to have [Java installed](https://www.java.com/en/download/) on your computer.)*

4.  If it succeeds, a new file named `my_body_data.fit` will appear in the folder.

### Step 6: Import to Garmin Connect
1.  Go to the Garmin Connect import page: [https://connect.garmin.com/modern/import-data](https://connect.garmin.com/modern/import-data)
2.  Drag your new `my_body_data.fit` file into the import box.
3.  Click "Import Data."

You're done! Your body composition data will now appear in your Garmin Connect profile under "Health Stats" > "Weight."
