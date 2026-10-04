FROM python:3.13-slim-bookworm@sha256:2325bb286ec344af3e5898cc224b5844e2707ac6e26b1632516fd3edc84a5e26
ENV PYTHONUNBUFFERED=1 PYTHONDONTWRITEBYTECODE=1 PIP_DISABLE_PIP_VERSION_CHECK=1
WORKDIR /app
COPY requirements.lock ./
RUN pip install --no-cache-dir -r requirements.lock
COPY tools ./tools
RUN python tools/fetch_frp.py frpc
COPY shared ./shared
COPY client ./client
COPY DOCS.md ./DOCS.md
COPY run.sh /run.sh
RUN chmod 755 /run.sh
HEALTHCHECK --interval=30s --timeout=5s --start-period=240s CMD ["python", "tools/healthcheck.py"]
CMD ["/run.sh"]
