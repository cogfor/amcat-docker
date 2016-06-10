# Elastic for AmCAT
#
# VERSION 20160609_1

FROM elasticsearch:1.7

MAINTAINER rene@cogfor.com

# Install plugins
RUN plugin -install elasticsearch/elasticsearch-analysis-icu/2.7.0
RUN plugin -install amcat/hitcount -url https://github.com/amcat/hitcount/releases/download/1.0/hitcount.zip 
#RUN plugin install https://github.com/amcat/hitcount/releases/download/1.0/hitcount.zip 
#RUN plugin install license -url https://download.elastic.co/elasticsearch/release/org/elasticsearch/plugin/license/2.3.3/license-2.3.3.zip
#RUN plugin install license 
RUN plugin install elasticsearch/marvel/latest -url https://download.elasticsearch.org/elasticsearch/marvel/marvel-2.3.3.tar.gz 
#RUN plugin install marvel-agent -url https://download.elasticsearch.org/elasticsearch/marvel/marvel-2.3.3.tar.gz
#RUN plugin install marvel-agent 
RUN plugin install lmenezes/elasticsearch-kopf/1.0
RUN plugin install mobz/elasticsearch-head/1.x

# Enable hitcount as default similarity provider, and enable groovy scripting
RUN echo "index.similarity.default.type: hitcountsimilarity" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "script.inline: on" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "script.update: on" >> /etc/elasticsearch/elasticsearch.yml
