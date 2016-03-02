FROM debian
RUN apt-get update
RUN apt-get install python2.7 python-pip -y
RUN mkdir app
RUN pip install flask
ADD app.py /app/
WORKDIR /app/
CMD ["python2.7","app.py"]