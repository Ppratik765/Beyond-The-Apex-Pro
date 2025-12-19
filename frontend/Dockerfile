# --- Stage 1: Build the React App ---
FROM node:18-alpine as build
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy source code and build
COPY . .
RUN npm run build

# --- Stage 2: Serve the App ---
# We use 'serve' to host the static files on the dynamic Railway port
FROM node:18-alpine
WORKDIR /app

# Install 'serve' globally
RUN npm install -g serve

# Copy the built 'dist' folder from the previous stage
COPY --from=build /app/dist ./dist

# Start the server on the port Railway provides
CMD serve -s dist -l $PORT
