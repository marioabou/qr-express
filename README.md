# QR Express

QR Express is a simple and efficient tool for generating QR codes for your website URLs. This project leverages HTML, CSS, and JavaScript to create a user-friendly interface for instant QR code generation.

## Table of Contents

- [Demo](#demo)
- [Features](#features)
- [Technologies](#technologies)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [JavaScript Functions](#javascript-functions)
- [Contributing](#contributing)
- [License](#license)

## Demo

You can access the live demo of the project here: [QR Express Demo](https://marioabou.github.io/qr-express)

## Features

- Generate QR codes for any URL
- Choose from multiple QR code sizes
- Download QR code images directly from the interface
- User-friendly and responsive design

## Technologies

- **Frontend:** HTML, CSS, JavaScript
- **QR Code Generation Library:** [qrcode.js](https://github.com/davidshimjs/qrcodejs)

## Installation

To run this project locally, follow these steps:

1. **Clone the repository:**
   ```sh
   git clone https://github.com/marioabou/qr-express.git
   ```
2. **Navigate to the project directory:**
   ```sh
   cd qr-express
   ```

## Usage

Open the `index.html` file in your browser to start using QR Express.

## Project Structure

```
qr-express/
├── css/
│   ├── styles.css
├── img/
│   ├── qr-code.png
├── js/
│   ├── script.js
├── index.html
└── README.md
```

- **index.html:** Main HTML file
- **css/styles.css:** Custom CSS styles
- **img/qr-code.png:** Default QR code image
- **js/script.js:** JavaScript file for QR code generation functionality

## JavaScript Functions

### onGenerateSubmit

This function handles the form submission, validates the URL input, shows the spinner, generates the QR code, and creates the save button.

```javascript
const onGenerateSubmit = (e) => {
  e.preventDefault();
  clearUI();
  const url = document.getElementById("url").value;
  const size = document.getElementById("size").value;
  if (url === "") {
    alert("Please enter a URL");
  } else {
    showSpinner();
    setTimeout(() => {
      hideSpinner();
      generateQRCode(url, size);
      showScanner();
      setTimeout(() => {
        const saveUrl = qr.querySelector("canvas").toDataURL();
        createSaveBtn(saveUrl);
      }, 50);
    }, 1000);
  }
};
```

### generateQRCode

This function generates the QR code using the `qrcode.js` library based on the provided URL and size.

```javascript
const generateQRCode = (url, size) => {
  const qrcode = new QRCode("qrcode", {
    text: url,
    width: size,
    height: size,
  });
};
```

### clearUI

This function clears the previous QR code and the save button from the UI.

```javascript
const clearUI = () => {
  qr.innerHTML = "";
  const saveBtn = document.getElementById("save-link");
  if (saveBtn) {
    saveBtn.remove();
  }
};
```

### showScanner

This function displays the QR code container.

```javascript
const showScanner = () => {
  const scanner = document.getElementById("qrCodeContainer");
  scanner.style.display = "block";
};
```

### showSpinner

This function shows the loading spinner.

```javascript
const showSpinner = () => {
  const spinner = document.getElementById("spinner");
  spinner.style.display = "block";
};
```

### hideSpinner

This function hides the loading spinner.

```javascript
const hideSpinner = () => {
  const spinner = document.getElementById("spinner");
  spinner.style.display = "none";
};
```

### createSaveBtn

This function creates a button to download the generated QR code as an image.

```javascript
const createSaveBtn = (saveUrl) => {
  const link = document.createElement("a");
  link.id = "save-link";
  link.classList = 'bg-red-500 hover:bg-red-700 text-white font-bold py-2 rounded w-1/3 m-auto my-5';
  link.innerHTML = "Save Image";
  link.href = saveUrl;
  link.download = "qrcode.png";
  document.getElementById("generated").appendChild(link);
};
```

### Download QR Code

```javascript
const downloadButton = document.getElementById("download-button");
downloadButton.addEventListener("click", () => {
  const qrCodeCanvas = document.querySelector("#qrcode canvas");
  const imageDataUrl = qrCodeCanvas.toDataURL("image/png");
  const link = document.createElement("a");
  link.href = imageDataUrl;
  link.download = "qrcode.png";
  link.click();
});
```

## Author: Mario Alberto Bouchot Osorio

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes.

## License

This project is licensed under the MIT License.
