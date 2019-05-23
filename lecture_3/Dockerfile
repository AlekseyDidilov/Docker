FROM python:3.6
WORKDIR /.
COPY hits/app.py ./
COPY requirements.txt ./
RUN mkdir +chmod logs && pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "./app.py"]



#docker build -t hits .
#docker tag hits didilovich/hits:h3
#docker push didilovich/hits:h3
#docker network create --driver=bridge task3
#docker run -itd --rm --net=task3 -p 5000:5000 didilovich/hits:h3
#docker run -itd --rm --name redis --net=task3 redis

#docker volume create db_log
#docker run -itd --rm --name hits --net=task3 -p 5000:5000 didilovich/hits:h3
#docker run -itd --rm --name redis -v  $(pwd)/db_log:/data   --net=task3 redis