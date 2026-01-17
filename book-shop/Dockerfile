# Use the official Python runtime image
FROM python:3.15-rc-slim
 
# Create the app directory
RUN mkdir /app
 
# Set the working directory inside the container
WORKDIR /app
 
# Set environment variables 
# Prevents Python from writing pyc files to disk
ENV PYTHONDONTWRITEBYTECODE=1
#Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1 
 
# Install system dependencies needed for cffi / zstandard
RUN apt-get update && apt-get install -y \
    gcc \
    build-essential \
    libffi-dev \
    python3-dev \
    curl \
 && rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip install --upgrade pip && pip install poetry

COPY pyproject.toml poetry.lock /app/
# Install dependencies instead of requirements.txt
RUN poetry install --no-root --only main

# Copy wheel and install it
COPY dist/*.whl /app/
RUN pip install --no-cache-dir *.whl
 
COPY . /app/
# Expose the Django port
EXPOSE 8000
 
# Run Django’s development server
CMD ["gunicorn", "book_shop.wsgi:application", "--bind", "0.0.0.0:8000"]
