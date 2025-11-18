FROM python:3.11-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Example envs; you’ll override in K8s via ConfigMap/Secret
ENV REDIS_HOST=redis \
    REDIS_PORT=6379

EXPOSE 5000

CMD ["python", "app.py"]

