# Official Nginx image
FROM nginx:alpine

# Copy static website files to Nginx web root
COPY . /usr/share/nginx/html

# Expose port 80 to outside world
EXPOSE 80

# Start Nginx when container starts
CMD ["nginx", "-g", "daemon off;"]
