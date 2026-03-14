# Use a lightweight Python image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file and install dependencies
# Note: You should have a requirements.txt file with 'flask' in it
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code (app.py, templates/, etc.)
COPY . .

# Expose the port the app runs on
EXPOSE 9000

# Run the application
CMD ["python", "app.py"]
