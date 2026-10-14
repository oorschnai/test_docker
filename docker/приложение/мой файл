FROM python:3.13-alpine

WORKDIR /site
COPY index.html .

EXPOSE 8080

CMD ["python", "-m", "http.server", "8080"]
