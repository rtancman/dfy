FROM django
  
RUN touch /usr/local/bin/eventex-entrypoint
RUN chmod +x /usr/local/bin/eventex-entrypoint

WORKDIR /var/www/html

ENTRYPOINT ["/usr/local/bin/eventex-entrypoint"]