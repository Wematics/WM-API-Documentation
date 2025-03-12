# Wematics Client Documentation

## Overview
The **Wematics API Client** enables users to access, retrieve, and process sky camera images, metadata, and related environmental data efficiently. This guide provides step-by-step instructions on installation, authentication, and usage.

## Installation
Ensure you have Python installed, then install the `wematics` package using pip:

```bash
pip install wematics
```

---

## Quick Start Guide

### 1. Authenticate and Initialize Client
```python
from wematics import Pyranocam

client = Pyranocam('YOUR_API_KEY')
cameras = client.list_cameras()
camera = cameras['cameras'][1]
print("Available cameras:", cameras['cameras'])
```

### 2. Retrieve Available Variables
```python
variables = client.list_variables(camera)
print(f"Variables for {camera}:", variables['variables'])
```

### 3. Fetch and Download Images

#### UTC Time Range
```python
images = client.list_images(camera, start="2025-01-01T17:00:00Z", end="2025-01-01T22:00:00Z")
client.download_images(images, save_path="./images")
```

#### Local Time Range
```python
images_local = client.list_images(camera, start_local="2025-01-01T17:00:00", end_local="2025-01-01T22:00:00")
client.download_images(images_local, save_path="./local_images")
```

---

## HDR Image Handling

### 4. Retrieve Available HDR Image Dates
```python
dates = client.list_dates(camera, "HDR")
day = dates['dates'][-2]
print("Available HDR Dates:", dates['dates'])
print("Selected day:", day)
```

### 5. Fetch HDR Files for a Specific Date (UTC)
```python
files = client.list_files(camera, "HDR", day, "utc")
file = files['files'][50]
print(f"Files for {camera}, HDR on {day}:", files['files'])
print("Total HDR files:", len(files['files']))
```

### 6. Download a Specific HDR File (UTC)
```python
client.download_file(camera, "HDR", file, timezone="utc")
```

### 7. Fetch and Download HDR Files (Local Time)
```python
files = client.list_files(camera, "HDR", day, "local")
file = files['files'][50]
print(f"Files for {camera}, HDR on {day}:", files['files'])
print("Total HDR files:", len(files['files']))
```

```python
client.download_file(camera, "HDR", file, timezone="local")
```

### 8. Bulk Download HDR Files in a Time Range (UTC)
```python
start_datetime = "2025-02-18_17_00_00"
end_datetime = "2025-02-18_17_05_00"
client.download_files_in_range(camera, "HDR", start_datetime, end_datetime, "", timezone="utc")
print(f"Files from {start_datetime} to {end_datetime} downloaded to ./downloads")
```

---

## Cloud Camera (CC) Image Handling

### 9. Fetch Available Cloud Camera (CC) Images
```python
files = client.list_files(camera, "CC", "2025-02-18")
file = files['files'][0]
print("Available CC files:", files['files'])
print("Selected file:", file)
```

---

## Downloading Measurement Data as CSV

### 10. Download CSV Data (UTC)
```python
client.download_csv(camera, start="2025-01-01T00:00:00Z", end="2025-01-02T00:00:00Z", save_path="./data_utc.csv")
```

### 11. Download CSV Data (Local Time)
```python
client.download_csv(camera, start_local="2025-01-01T00:00:00", end_local="2025-01-02T00:00:00", save_path="./data_local.csv")
```

---

## API Reference

### General API Methods

| Method | Description |
|--------|-------------|
| `list_cameras()` | Retrieves a list of available cameras. |
| `list_variables(camera)` | Lists variables available for the specified camera. |
| `list_images(camera, start, end)` | Lists available images within a specified UTC time range. |
| `download_images(image_list, save_path)` | Downloads selected images to a local directory. |

### HDR Image Handling

| Method | Description |
|--------|-------------|
| `list_dates(camera, image_type)` | Lists available dates for a specific image type. |
| `list_files(camera, image_type, date, timezone='utc')` | Retrieves available image files for a given date. |
| `download_file(camera, image_type, file, timezone='utc')` | Downloads a specified image file. |
| `download_files_in_range(camera, image_type, start_datetime, end_datetime, save_path, timezone='utc')` | Downloads images in a defined time range. |

### CSV Data Retrieval

| Method | Description |
|--------|-------------|
| `download_csv(camera, start, end, save_path)` | Retrieves measurement data as a CSV file. |

---

## Frequently Asked Questions (FAQ)

### 1. How do I get my API key?
- Your API key is provided when you register with Wematics. If lost, request a new one via support.

### 2. Can I use the API without authentication?
- No, authentication via an API key is mandatory.

### 3. What time format should I use for time-based queries?
- Use **ISO 8601** for UTC (e.g., `"2025-01-01T17:00:00Z"`).
- For local time queries, use `"YYYY-MM-DD HH:MM:SS"`.

### 4. What is the difference between HDR and CC?
- **HDR (High Dynamic Range)**: Sky imagery with enhanced contrast for better cloud detection.
- **CC (Cloud Cover)**: Cloud cover retrieveed from sky images in % and oktas.

---

## Support
For any issues, inquiries, or bug reports, please contact Wematics support or visit our [website](https://www.wematics.com).

---

## License
This project is licensed under the **MIT License**.
