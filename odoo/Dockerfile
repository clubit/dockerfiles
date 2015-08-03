FROM odoo
MAINTAINER Jan Vereecken <janvereecken@clubit.be>

USER root

RUN apt-get update
RUN set -x; \
        apt-get install -q -y build-essential gcc git-core python-dev vim-nox wget \
        && wget https://bootstrap.pypa.io/get-pip.py \
        && python get-pip.py \
        && pip install cython \
        && git clone https://github.com/dsuch/gevent.git && cd gevent && python setup.py install && cd .. \
        && pip install grequests \
        && pip install -e git://github.com/jdunck/python-unicodecsv.git#egg=unicodecsv \
        && pip install xmltodict

# Expose Odoo services
EXPOSE 8069 8071

# Set the default config file
ENV OPENERP_SERVER /etc/odoo/openerp-server.conf

# Set default user when running the container
USER odoo

ENTRYPOINT ["/entrypoint.sh"]
CMD ["openerp-server"]