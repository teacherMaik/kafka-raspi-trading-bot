# Use a lightweight Python image compatible with ARM64 (Raspberry Pi)
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Install system dependencies (minimal for PRAW/Kafka)
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    python3-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy only the requirements first to leverage Docker layer caching
COPY requirements.txt .

# Install Python libraries
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of your ingestion code (scraper.py, etc.)
COPY . .

# Start the scraper
CMD ["python", "scraper.py"]