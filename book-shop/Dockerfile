# Use the official Python runtime image
FROM python:3.15.0a2-slim-trixie
 
# Create the app directory
RUN mkdir /app
 
# Set the working directory inside the container
WORKDIR /book-shop
 
# Set environment variables 
# Prevents Python from writing pyc files to disk
ENV PYTHONDONTWRITEBYTECODE=1
#Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1 
 
# Upgrade pip
RUN pip install --upgrade pip 
 
# Copy the Django project  and install dependencies
COPY requirements.txt  /app/
 
# run this command to install all dependencies 
RUN pip install --no-cache-dir -r requirements.txt
 
WORKDIR /app

# Copy wheel and install it
COPY dist/*.whl /app/
RUN pip install --no-cache-dir *.whl
 
COPY . /app/
# Expose the Django port
EXPOSE 8000
 
# Run Django’s development server
CMD ["gunicorn", "book_shop.wsgi:application", "--bind", "0.0.0.0:8000"]
