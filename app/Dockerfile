FROM python:3.11-slim

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir flask

# ✅ Create non-root user
RUN useradd -m appuser

# ✅ Switch to non-root
USER appuser

CMD ["python", "app.py"]