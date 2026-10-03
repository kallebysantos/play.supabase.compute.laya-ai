FROM public.ecr.aws/docker/library/python:3.14-slim

WORKDIR /app

COPY requirements.txt requirements.txt

RUN pip install --no-cache-dir torch --index-url https://download.pytorch.org/whl/cpu
RUN pip install --no-cache-dir -r requirements.txt

# Prefetch the Laya English checkpoint during build
RUN python -c "import laya; laya.load('convaiinnovations/laya', device='cpu')"

COPY main.py .

# workers-infra default maps to PORT=8080, defining on Dockerfile as fallback
ARG PORT=8080
ENV PORT=${PORT}

EXPOSE ${PORT}

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
