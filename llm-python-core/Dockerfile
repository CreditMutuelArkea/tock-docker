FROM python:3

WORKDIR /code

RUN python -m venv /opt/venv

# Make sure we use the virtualenv:
ENV PATH="/opt/venv/bin:$PATH"

COPY target/requirements.txt .

RUN pip install -r requirements.txt

COPY target/app /code/app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]