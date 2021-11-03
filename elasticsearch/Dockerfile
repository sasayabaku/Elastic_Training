FROM docker.elastic.co/elasticsearch/elasticsearch:7.15.0
RUN elasticsearch-plugin install analysis-kuromoji

COPY ./config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml