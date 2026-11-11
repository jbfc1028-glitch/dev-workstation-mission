FROM alpine:latest

WORKDIR /app

COPY app.sh .

RUN echo "This file was created during docker build." > build-info.txt

CMD ["sh", "app.sh"]