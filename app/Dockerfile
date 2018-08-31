FROM python:3.7

ENV MATHICS_HOME=/usr/src/app
ENV ENTRYPOINT_COMMAND="docker run -it {MATHICS_IMAGE}"

WORKDIR $MATHICS_HOME

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

RUN groupadd mathics && \
    useradd -d $MATHICS_HOME -g mathics -m -s /bin/bash mathics && \
    mkdir -p $MATHICS_HOME/data && \
    chown -R mathics:mathics $MATHICS_HOME

USER mathics

ENTRYPOINT ["/entrypoint.sh"]

CMD ["--help"]
