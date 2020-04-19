FROM ruby:2.7

RUN gem install mailcatcher

ARG SMTP_PORT
ARG HTTP_PORT

EXPOSE $SMTP_PORT $HTTP_PORT

RUN echo "SMTP Port: $SMTP_PORT"
RUN echo "HTTP Port: $HTTP_PORT"

ENTRYPOINT ["mailcatcher", "-f"]

CMD ["--ip", "0.0.0.0"]
