# Summary

* [Overview](overview.md)
    * [Navigating CORD](navigate.md)
    * [Quick Start](quickstart.md)
        * [MacOS](macos.md)
        * [Linux](linux.md)
* [Installation Guide](README.md)
    * [Prerequisites](prereqs/README.md)
        * [Hardware Requirements](prereqs/hardware.md)
        * [Connectivity Requirements](prereqs/networking.md)
        * [Software Requirements](prereqs/software.md)
            * [Kubernetes](prereqs/kubernetes.md)
                * [Single Node](prereqs/k8s-single-node.md)
                * [Multi-Node](prereqs/k8s-multi-node.md)
            * [Helm](prereqs/helm.md)
            * [Optional Packages](prereqs/optional.md)
                * [Docker Registry](prereqs/docker-registry.md)
                * [OpenStack](prereqs/openstack-helm.md)
    * [Fabric Software Setup](fabric-setup.md)
    * [Bringing Up CORD](profiles/intro.md)
        * [R-CORD](profiles/rcord/install.md)
            * [EdgeCore (OpenOLT driver) Setup](openolt/README.md)
            * [Celestica / Microsemi Setup](profiles/rcord/celestica-olt-setup.md)
            * [Emulated OLT/ONU](profiles/rcord/emulate.md)
        * [M-CORD](profiles/mcord/install.md)
            * [EnodeB Setup](profiles/mcord/enodeb-setup.md)
    * [Helm Reference](charts/helm.md)
        * [XOS-CORE](charts/xos-core.md)
        * [ONOS](charts/onos.md)
        * [VOLTHA](charts/voltha.md)
        * [Kafka](charts/kafka.md)
        * [Hippie OSS](charts/hippie-oss.md)
        * [Base OpenStack](charts/base-openstack.md)
            * [VTN Setup](prereqs/vtn-setup.md)
        * [R-CORD](charts/rcord.md)
        * [M-CORD](charts/mcord.md)
        * [XOSSH](charts/xossh.md)
        * [Logging and Monitoring](charts/logging-monitoring.md)
        * [Persistent Storage](charts/storage.md)
* [Operations Guide](operating_cord/operating_cord.md)
    * [General Info](operating_cord/general.md)
        * [GUI](operating_cord/gui.md)
            * [Configuring the Service Graph](xos-gui/developer/service_graph.md)
        * [REST API](operating_cord/rest_apis.md)
        * [TOSCA](xos-tosca/README.md)
        * [XOSSH](xos/dev/xossh.md)
        * [XOS Internals](operating_cord/xos_internals.md)
            * [XOS Containers](xos/xos_internals.md)
            * [XOS Configuration](xos/modules/xosconfig.md)
    * [Configuring Profiles](operating_cord/profiles.md)
        * [R-CORD](profiles/rcord/configuration.md)
            * Workflows
                * [AT&T](profiles/rcord/workflows/att.md)
        * [M-CORD](profiles/mcord/configuration.md)
    * [Configuring Services](operating_cord/services.md)
        * [Fabric](fabric/README.md)
        * [ONOS](onos-service/README.md)
        * [RCORD](rcord/README.md)
        * [vOLT](olt-service/README.md)
        * [vRouter](vrouter/README.md)
        * [AT&T Workflow Driver](att-workflow-driver/README.md)
    * [Attach containers to external NICs](operating_cord/veth_intf.md)
* [Development Guide](developer/developer.md)
    * [Getting the Source Code](developer/getting_the_code.md)
    * [Writing Models and Synchronizers](xos/intro.md)
        * [XOS Modeling Framework](xos/dev/xproto.md)
            * [XOS Tool Chain (Internals)](xos/dev/xosgenx.md)
        * [XOS Synchronizer Framework](xos/dev/synchronizers.md)
            * [Synchronizer Design](xos/dev/sync_arch.md)
            * [Synchronizer Implementation](xos/dev/sync_impl.md)
            * [Synchronizer Reference](xos/dev/sync_reference.md)
        * [Core Models](xos/core_models.md)
        * [Security Policies](xos/security_policies.md)
        * [Tutorial](xos/tutorials/basic_synchronizer.md)
        * [Build proto files from xProto](xos/dev/xproto_to_protobuf.md)
    * [Developer Workflows](developer/workflows.md)
        * [Working on R-CORD Without an OLT/ONU](developer/configuration_rcord.md)
    * [Building Docker Images](developer/imagebuilder.md)
    * [Platform Services](developer/platform.md)
        * [Kubernetes](kubernetes-service/kubernetes-service.md)
        * [OpenStack](openstack/openstack-service.md)
        * [VTN and Service Composition](xos/xos_vtn.md)
    * [Example Services](examples/examples.md)
        * [SimpleExampleService](simpleexampleservice/simple-example-service.md)
        * [ExampleService](exampleservice/example-service.md)
    * [GUI Development](xos-gui/developer/README.md)
        * [Quickstart](xos-gui/developer/quickstart.md)
        * [GUI Extensions](xos-gui/developer/gui_extensions.md)
        * [GUI Internals](xos-gui/architecture/README.md)
            * [Module Strucure](xos-gui/architecture/gui-modules.md)
            * [Data Sources](xos-gui/architecture/data-sources.md)
        * [Tests](xos-gui/developer/tests.md)
    * [Unit Tests](xos/dev/unittest.md)
    * [Versions and Releases](versioning.md)
* [Testing Guide](cord-tester/README.md)
    * [Test Setup](cord-tester/qa_testsetup.md)
    * [Test Environment](cord-tester/qa_testenv.md)
    * [System Tests](cord-tester/validate_pods.md)

