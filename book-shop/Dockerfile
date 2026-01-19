# Use the official Python runtime image
FROM python:3.15-rc-slim
 
# Set the working directory inside the container
WORKDIR /app
 
# Set environment variables 
# Prevents Python from writing pyc files to disk
ENV PYTHONDONTWRITEBYTECODE=1
#Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1 
 
# COPY pyproject.toml poetry.lock /app/
# # Install dependencies instead of requirements.txt
# RUN poetry install --no-root --only main

# Copy wheel and install it
COPY *.whl /app/

RUN pip install /app/*.whl
 
# Expose the Django port
EXPOSE 4000
EXPOSE 3000

# Run Django’s development server
ENTRYPOINT ["gunicorn"]
CMD ["book_shop.wsgi:application", "--bind", "0.0.0.0:4000"]
