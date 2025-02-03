# Node.js resmi imajını kullan
FROM node:18-alpine

# Çalışma dizinini belirle
WORKDIR /app

# Bağımlılıkları yükle
COPY package.json package-lock.json ./
RUN npm install --only=production

# Uygulama dosyalarını kopyala
COPY . .

# Port aç
EXPOSE 3000

# Uygulamayı başlat
CMD ["npm", "start"]
