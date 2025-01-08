
# README: Challenges Walkthrough

## Challenge 1: UART Data Analysis

### Problem Statement
Analyze UART communication data using a tool like PulseView to extract meaningful information such as the baud rate and decode the transmitted data to uncover the hidden flag.

### Steps to Solve:

#### 1. Open File in PulseView
   - Load the given UART data file into the PulseView software.

#### 2. Determine Baud Rate
   - Use a bitrate analyzer in PulseView or measure the duration of one bit in the signal.
   - If manually measured, compute the baud rate using the formula:
     \[
     \text{Baud Rate} = \frac{1}{\text{Time per Bit}}
     \]
   - Expected baud rate: **5333333 b/s**.

#### 3. Decode Using UART Decoder
   - Set up the UART decoder in PulseView with the determined baud rate and other correct parameters (e.g., parity, stop bits).
   - Analyze the decoded data to extract the flag.

### Tools Used:
- **PulseView**: For visualizing and decoding UART data.
- **Bitrate Analyzer**: To measure or confirm the baud rate.

### Key Takeaway:
Precise baud rate measurement is critical for accurate decoding. Any mismatch leads to erroneous results.

---

## Challenge 2: "Farewell Firewall"

### Problem Statement
Analyze network logs to detect anomalies, uncover hidden data through XOR operations, and extract the flag by converting binary operations into meaningful ASCII characters.

### Steps to Solve:

#### Step 1: DBSCAN for Outlier Detection
   - **Objective**: Identify anomalies in the dataset.
   - **Procedure**:
     1. Load the dataset (`Network_Log.csv`) containing latitude and longitude data.
     2. Standardize the data using `StandardScaler`.
     3. Apply the DBSCAN clustering algorithm to detect dense clusters and outliers.
     4. Save the outlier data for further analysis.

   - **Code Snippet**:
     ```python
     import pandas as pd
     from sklearn.preprocessing import StandardScaler
     from sklearn.cluster import DBSCAN
     import matplotlib.pyplot as plt

     # Load the dataset
     df = pd.read_csv('Network_Log.csv')

     # Extract coordinates
     coordinates = df[['latitude_coord', 'longitude_coord']]
     
     # Standardize data
     scaler = StandardScaler()
     coordinates_scaled = scaler.fit_transform(coordinates)

     # Apply DBSCAN
     dbscan = DBSCAN(eps=0.1, min_samples=6)
     df['outlier'] = dbscan.fit_predict(coordinates_scaled)

     # Save and visualize
     df[df['outlier'] == -1].to_csv('outliers.csv', index=False)
     plt.scatter(df['latitude_coord'], df['longitude_coord'], c=df['outlier'], cmap='coolwarm')
     plt.show()
     ```
   - **Outcome**: Detected and isolated 58 outliers representing tampered data entries.

#### Step 2: XOR Data Analysis
   - **Objective**: Balance the "energy flow" (data downloaded vs. uploaded) using XOR.
   - **Procedure**:
     1. Perform an XOR operation between `data_downloaded` and `data_uploaded`.
     2. Convert the result into ASCII characters to extract hidden information.

   - **Code Snippet**:
     ```python
     def xor_and_to_ascii(row):
         try:
             result = int(row['data_downloaded']) ^ int(row['data_uploaded'])
             return chr(result)
         except ValueError:
             return ''

     df['xored_ascii'] = df.apply(xor_and_to_ascii, axis=1)
     df.to_csv('xor.csv', index=False)
     ```
   - **Outcome**: Generated an ASCII column with readable characters from the XOR operation.

#### Step 3: Sorting and Final Flag Extraction
   - **Objective**: Align extracted data using `user_id` for meaningful interpretation.
   - **Procedure**:
     1. Sort the outlier data by `user_id`.
     2. Concatenate the ASCII values to form the final flag.

   - **Code Snippet**:
     ```python
     df_sorted = df.sort_values(by='user_id')
     print(" ".join(df_sorted['xored_ascii'].astype(str)))
     ```
   - **Outcome**: Reconstructed the hidden flag.

### Key Insights:
1. **Anomaly Detection:** DBSCAN effectively identifies manipulated or hidden entries.
2. **XOR Operations:** A powerful tool for revealing hidden patterns.
3. **Sorting:** Ensures logical sequencing for correct flag extraction.

---

### Tools Used:
- **Python Libraries:** Pandas, scikit-learn, matplotlib.
- **DBSCAN Algorithm:** For outlier detection.
- **ASCII Conversion:** For decoding hidden information.

### Lessons Learned:
- Attention to detail in parameter selection (e.g., DBSCAN's `eps` and `min_samples`) is crucial.
- Proper data preprocessing and interpretation lead to successful extraction of the flag.
