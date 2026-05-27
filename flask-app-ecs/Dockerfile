#base image
FROM python:3.14-slim

#create dir
WORKDIR /app

#COPY src code to cntr
COPY . .

#run command
RUN pip install -r requirements.txt

EXPOSE 80

CMD ["python", "run.py"]
