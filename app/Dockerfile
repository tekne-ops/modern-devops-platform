FROM python:3.11-alpine

WORKDIR /app

COPY . .

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ✅ Create non-root user
RUN adduser -D appuser

# ✅ Switch to non-root
USER appuser

CMD ["python", "app.py"]