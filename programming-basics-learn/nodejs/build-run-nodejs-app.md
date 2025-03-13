# How to Build and Run Javascript (NodeJS) App and Host on NGINX server

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/mir-owahed/devsecops-demo.git
   cd devsecops-demo
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn
   ```

3. Start the development server:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

## Building for Production

To create a production build:

```bash
npm run build
# or
yarn build
```

The build artifacts will be stored in the `dist/` directory.

## Host on NGINX server

 ```bash
 sudo apt install nginx -y
sudo cp -r dist*/ /var/www/html/
sudo cp -r dist*/ /var/www/html/
cd /var/www/html/
cd dist/
ls
sudo cp -r assets/ index.html ../
systemctl restart nginx
   ```
Open your browser and navigate to `http://localhost:80`
