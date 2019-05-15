FROM jfloff/alpine-python
WORKDIR /flask .
COPY app.py ./ 
COPY index.html templates/
RUN pip install --upgrade pip && pip install flask
EXPOSE 5000
CMD ["python", "./app.py"]
