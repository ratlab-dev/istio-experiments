# Independent Clusters Istio Demo

This repository provides resources and examples for deploying and managing multiple independent Kubernetes clusters with [Istio](https://istio.io/) service mesh. It includes sample manifests, Helm charts, Ansible playbooks, and configuration files to help you set up, test, and tear down Istio-enabled clusters for experimentation, development, or demonstration purposes.

## Directory Structure

- `pod.yaml`  
  Example Kubernetes Pod manifest.

- `ansible/`  
  Ansible playbooks and inventory for automating cluster setup and teardown.
  - `prerequisites.yaml` – Playbook to download and extract the Istio release.
  - `create.yaml` – Playbook to create resources.
  - `teardown.yaml` – Playbook to remove resources.
  - `vars.yaml` – Variable definitions.
  - `inventory` – Inventory file for Ansible.

- `istio-1.16.2/`  
  Istio release directory containing:
  - `README.md` – Istio documentation and usage.
  - `LICENSE` – License information (Apache 2.0).
  - `manifest.yaml` – Istio manifest.
  - `bin/istioctl` – Istio CLI tool.
  - `manifests/` – Helm charts and sample manifests for Istio components.
  - `samples/` – Example applications and configurations (e.g., Bookinfo, Helloworld, Addons).
  - `tools/` – Utility scripts and tools.

- `kind/`  
  Example [kind](https://kind.sigs.k8s.io/) cluster configuration files.
  - `cluster-hdc.yaml`
  - `cluster-mdc.yaml`

- `manifests/`  
  Additional Kubernetes manifests.
  - `metallb-manifests.yaml` – Example MetalLB configuration.
  - `echo/` – Echo service manifests.

- `metallb/`  
  MetalLB configuration templates.
  - `IPAddressPool.yaml.j2`
  - `L2Advertisement.yaml`

## Getting Started

1. **Run Prerequisites**  
   Download all dependencies required for the setup:
   ```sh
   ansible-playbook ansible/prerequisites.yaml
   ```
   This will download Istio version 1.16.2 and extract it to the project directory.

2. **Create Clusters and Deploy Services**  
   Use the create playbook to:
   - Create the required Kubernetes clusters (using kind)
   - Install MetalLB
   - Install Istio
   - Deploy the sample service in both clusters
   ```sh
   ansible-playbook ansible/create.yaml
   ```

3. **Teardown**  
   To delete the clusters and clean up all resources, run:
   ```sh
   ansible-playbook ansible/teardown.yaml
   ```

> **Note:**  
> Do not manually test or modify anything in the `istio-1.16.2/` directory. All setup, installation, and teardown should be performed using the provided Ansible playbooks.

## License

This repository and included Istio resources are licensed under the [Apache License 2.0](istio-1.16.2/LICENSE).

## References

- [Istio Documentation](https://istio.io/)
- [Bookinfo Sample](istio-1.16.2/samples/bookinfo/README.md)
- [Helloworld Sample](istio-1.16.2/samples/helloworld/README.md)
- [Istio Addons](istio-1.16.2/samples/addons/README.md)