# Build stage for trame WASM VTK application
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libgl1 \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libgomp1 \
    libosmesa6 \
    libegl1 \
    libgles2 \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for better caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application files and data
COPY app.py .
COPY *.vtp *.vtu *.jpg *.gif . /app/

# Expose trame default port
EXPOSE 8080

# Run the application
CMD ["python", "app.py", "--port", "8080", "--server"]
