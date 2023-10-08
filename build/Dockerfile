FROM python:3.9-slim-buster

LABEL Name="Python Flask Demo App" 
LABEL org.opencontainers.image.source = "https://github.com/darktang3nt69/python-demoapp-e2e"

ARG srcDir=src
WORKDIR /app
COPY $srcDir/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY $srcDir/run.py .
COPY $srcDir/app ./app

EXPOSE 5000

CMD ["gunicorn", "-b", "0.0.0.0:5000", "run:app"]