# Creates the minimum environment to package and run this Skyve application.
# Note that this uses an in-memory database and is only useful for demonstration/development.
FROM bizhubaustralia/skyve-wildfly:32.0.1.Final

ENV LANG en_US.UTF-8

USER root
RUN mkdir /content
RUN chown jboss:jboss /content

RUN mkdir -p /opt/skyve/addins/
RUN chown jboss:jboss /opt/skyve/addins/

USER jboss
ADD skyve-content-9.0.0.zip /opt/skyve/addins/skyve-content-9.0.0.zip
ADD maiasObligationsRegister.war /opt/jboss/wildfly/standalone/deployments/maiasObligationsRegister.war
ADD maiasObligationsRegister.json /opt/jboss/wildfly/standalone/deployments
RUN touch /opt/jboss/wildfly/standalone/deployments/maiasObligationsRegister.war.dodeploy

ENV SKYVE_CONTENT='/content/' \
    SKYVE_DATASTORE_DIALECT='org.skyve.impl.persistence.hibernate.dialect.H2SpatialDialect' \
    DATABASE_URL='maiasObligationsRegister_db' \
    SKYVE_SECURITY_DOMAIN_NAME='maiasObligationsRegister' \
    SKYVE_JNDI_NAME='maiasObligationsRegisterDB'

ENTRYPOINT [ "entrypoint.sh" ]
CMD [ "/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-Djava.locale.providers=COMPAT,CLDR" ]
