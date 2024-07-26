# Using "-slim", debian alternative because of :
# - need to support ONNX that isn't compiled for Alpine / ManyLinux architectures see this comment : https://github.com/microsoft/onnxruntime/issues/2909#issuecomment-593591317
FROM python:3.11-slim

WORKDIR /app

COPY target/requirements.txt .

ENV HTTP_PROXY="http://172.17.0.1:3128"
ENV HTTPS_PROXY="http://172.17.0.1:3128"
ENV http_proxy="http://172.17.0.1:3128"
ENV https_proxy="http://172.17.0.1:3128"

# build-essential required for llama-cpp
RUN apt update && apt install -y git build-essential
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt --use-deprecated=legacy-resolver

RUN unset HTTP_PROXY
RUN unset HTTPS_PROXY
RUN unset http_proxy
RUN unset https_proxy

COPY target/gen_ai_orchestrator gen_ai_orchestrator/

EXPOSE 8000

CMD ["uvicorn", "gen_ai_orchestrator.main:app", "--host", "0.0.0.0", "--port", "8000", "--log-config", "gen_ai_orchestrator/configurations/logging/config.ini"]