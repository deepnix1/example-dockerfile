Example Dockerfile Project
This project demonstrates how to use a basic Dockerfile to containerize a simple Node.js application.

Prerequisites
Make sure you have the following installed:

Docker
Node.js
Setup
Clone the repository:

bash
Kopyala
Düzenle
git clone https://github.com/deepnix1/example-dockerfile.git
cd example-dockerfile
Install dependencies:

bash
Kopyala
Düzenle
npm install
Build the Docker image:

bash
Kopyala
Düzenle
docker build -t example-dockerfile .
Run the Docker container:

bash
Kopyala
Düzenle
docker run -p 3000:3000 example-dockerfile
Access the application by navigating to http://localhost:3000 in your browser.

License
This project is licensed under the MIT License - see the LICENSE file for details.
