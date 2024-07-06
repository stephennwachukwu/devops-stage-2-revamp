FROM python:3.10-slim

# Install curl and other dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH
ENV PATH="${PATH}:/root/.local/bin"

# Set working directory
WORKDIR /app

# Copy only the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock* ./

# Install dependencies using Poetry
RUN poetry install --no-root

# Copy the rest of the application code
COPY . .

# Set environment variables
ENV DOMAIN=localhost \
    ENVIRONMENT=local \
    PROJECT_NAME="Full Stack FastAPI Project" \
    STACK_NAME=full-stack-fastapi-project \
    BACKEND_CORS_ORIGINS="http://localhost,http://localhost:5173,https://localhost,https://localhost:5173,http://localhost:3000" \
    SECRET_KEY=changethis123 \
    FIRST_SUPERUSER=devops@hng.tech \
    FIRST_SUPERUSER_PASSWORD=devops#HNG11 \
    USERS_OPEN_REGISTRATION=True \
    SMTP_HOST= \
    SMTP_USER= \
    SMTP_PASSWORD= \
    EMAILS_FROM_EMAIL=info@example.com \
    SMTP_TLS=True \
    SMTP_SSL=False \
    SMTP_PORT=587 \
    POSTGRES_SERVER=localhost \
    POSTGRES_PORT=5432 \
    POSTGRES_DB=app \
    POSTGRES_USER=app \
    POSTGRES_PASSWORD=changethis123

# Make the prestart script executable
RUN chmod +x ./prestart.sh
#RUN poetry run bash ./prestart.sh


# Expose port 8000 (assuming your backend server runs on this port)
EXPOSE 8000

# Command to run the backend server 
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
# CMD ["bash", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]
