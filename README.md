Wematics Client Documentation

Overview

Wematics provides an API client for accessing and downloading sky camera images, metadata, and related data. This guide explains how to install and use the wematics Python package.

Installation

Ensure you have Python installed, then install the wematics package using pip:

pip install wematics

Quick Start

1. Import and Authenticate

from wematics import Pyranocam

client = Pyranocam('YOUR_API_KEY')
cameras = client.list_cameras()
camera = cameras['cameras'][1]
print("Available cameras:", cameras['cameras'])

2. List Available Variables

variables = client.list_variables(camera)
print(f"Variables for {camera}:", variables['variables'])

3. List and Download Images

UTC Time Range

images = client.list_images(camera, start="2025-01-01T17:00:00Z", end="2025-01-01T22:00:00Z")
client.download_images(images, save_path="./images")

Local Time Range

images_local = client.list_images(camera, start_local="2025-01-01T17:00:00", end_local="2025-01-01T22:00:00")
client.download_images(images_local, save_path="./local_images")

4. Download CSV Files

UTC Data

client.download_csv(camera, start="2025-01-01T00:00:00Z", end="2025-01-02T00:00:00Z", save_path="./data_utc.csv")

Local Data

client.download_csv(camera, start_local="2025-01-01T00:00:00", end_local="2025-01-02T00:00:00", save_path="./data_local.csv")

API Reference

list_cameras()

Returns a list of available cameras.

list_variables(camera)

Returns the list of variables available for the specified camera.

list_images(camera, start, end)

Lists images available within a specific UTC time range.

download_images(image_list, save_path)

Downloads images to the specified local directory.

download_csv(camera, start, end, save_path)

Downloads measurement data as a CSV file.

Support

For any issues or inquiries, please contact Wematics support or visit our website.

License

This project is licensed under the MIT License.
