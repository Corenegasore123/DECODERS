# Barcode Decoder Collection

Collection of small Python utilities to decode barcodes and 2D codes (QR, Data Matrix, PDF417, and generic barcodes) with helper images and Java ZXing jars for PDF417.

## Repo layout

- [barcode-decoder/barcode-decoder.py](barcode-decoder/barcode-decoder.py) — Universal barcode decoder using OpenCV + pyzbar. See [`barcode_decoder.decode_all_barcodes`](barcode-decoder/barcode-decoder.py) for the main function.
- [barcode-decoder/barcode.png](barcode-decoder/barcode.png) — Example barcode image.
- [data-matrix-decoder/decode_data_matrix_code.py](data-matrix-decoder/decode_data_matrix_code.py) — Data Matrix decoder using pylibdmtx + PIL + OpenCV. See [`decode_data_matrix_code.decode_datamatrix`](data-matrix-decoder/decode_data_matrix_code.py).
- [pdf-417-decoder/decode_barcode.py](pdf-417-decoder/decode_barcode.py) — PDF417 decoding wrapper that invokes ZXing inside Docker (requires Java jars). See [`decode_barcode`](pdf-417-decoder/decode_barcode.py).
- [pdf-417-decoder/core-3.5.0.jar](pdf-417-decoder/core-3.5.0.jar) — ZXing core jar (bundled).
- [pdf-417-decoder/javase-3.5.0.jar](pdf-417-decoder/javase-3.5.0.jar) — ZXing javase jar (bundled).
- [pdf-417-decoder/jcommander-1.82.jar](pdf-417-decoder/jcommander-1.82.jar) — JCommander jar (bundled).
- [pdf-417-decoder/image.png](pdf-417-decoder/image.png) — Example PDF417 image.
- [qr-code-decoder/qr_code_decoder.py](qr-code-decoder/qr_code_decoder.py) — QR code decoder using pyzbar + OpenCV. See [`qr_code_decoder.decode_qr_code`](qr-code-decoder/qr_code_decoder.py).
- [qr-code-decoder/qrcode.png](qr-code-decoder/qrcode.png) — Example QR code image.

## Requirements

- Python 3.8+
- OpenCV (cv2)
- pyzbar
- pylibdmtx
- Pillow (PIL)
- Docker (only required to run the PDF417 ZXing Docker command)
- If running PDF417 via the included jars without Docker, a Java 17+ runtime is required.

Install Python dependencies (example):

```sh
pip install opencv-python pyzbar pylibdmtx Pillow
```

## Usage

- QR codes:

  - Run the script: python [qr-code-decoder/qr_code_decoder.py](qr-code-decoder/qr_code_decoder.py)
  - Main callable: [`qr_code_decoder.decode_qr_code`](qr-code-decoder/qr_code_decoder.py)

- Data Matrix:

  - Run the script: python [data-matrix-decoder/decode_data_matrix_code.py](data-matrix-decoder/decode_data_matrix_code.py)
  - Main callable: [`decode_data_matrix_code.decode_datamatrix`](data-matrix-decoder/decode_data_matrix_code.py)

- Generic barcodes (EAN, UPC, etc.):

  - Run the script: python [barcode-decoder/barcode-decoder.py](barcode-decoder/barcode-decoder.py)
  - Main callable: [`barcode_decoder.decode_all_barcodes`](barcode-decoder/barcode-decoder.py)

- PDF417 (ZXing via Docker):
  - Ensure Docker is running.
  - Run the script: python [pdf-417-decoder/decode_barcode.py](pdf-417-decoder/decode_barcode.py)
  - This script mounts the current folder into a Java container and runs ZXing’s `CommandLineRunner`. It expects the bundled jars and [pdf-417-decoder/image.png](pdf-417-decoder/image.png).

## Notes

- The OpenCV windows created by these scripts will block until a key is pressed.
- If a decoder fails to find codes, try increasing image contrast, cropping, or rotating the input image.
- The PDF417 script depends on ZXing output parsing; adjust parsing if you use a different ZXing version.
