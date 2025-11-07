Architecture
============

For more details about the architecture and its use of Docker, see the `LabCAS Docker Documentation`_.


Architecture Diagram
--------------------

.. mermaid::
    :caption: LabCAS Architecture within a Docker Composition
    :align: center
    :zoom:

    flowchart TD
        subgraph labcas-net[Docker Network: labcas-net]
            ldap[(LDAP)]
            backend[(LabCAS Backend)]
            ui[(LabCAS UI)]
            mockauth[(Mock Auth)]
            proxy[(LabCAS Proxy)]
            postgres[(Postgres DB)]
            airflow[(Airflow)]
            publish[(Publish Service)]
        end

        %% External Users
        user[End User] -->|HTTP/HTTPS| proxy
        proxy --> ui
        proxy --> backend

        %% Internal Dependencies
        ui --> backend
        backend --> ldap
        mockauth --> backend
        mockauth --> ui
        airflow --> backend
        airflow --> postgres
        publish --> backend

        %% Volumes
        backend --- vol1[(labcas-solr-index Volume)]
        postgres --- vol2[(postgres-data Volume)]


Architecture Details
--------------------

The LabCAS architecture is composed of the following components:

• LDAP: LDAP is used for authentication and authorization.
• LabCAS Backend: The LabCAS backend is the core component of the system. It is responsible for the data storage and retrieval.
• LabCAS UI: The LabCAS UI is the web interface for the system.
• Mock Auth: Mock Auth is used for authentication and authorization.
• LabCAS Proxy: The LabCAS proxy is used to route requests to the backend.
• Postgres: Postgres is used for data storage.
• Airflow: Airflow is used for workflow management.
• Publish Service: The Publish Service is used to publish the data to the web.

More TBD.


.. References:
.. _`LabCAS Docker Documentation`: https://github.com/Labcas-NIST/labcas-docker/