FROM python:3.11-alpine
WORKDIR /usr/local/app
COPY . .
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
CMD ["python3", "requirements.txt"]
