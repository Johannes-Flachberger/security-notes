---
tags:
  - "#type/tech-specific"
---
# Fundamentals

Also called dependency confusion or dependency hijacking.

Some package managers like npm or PyPi (pip) prioritize newer package versions over older ones, if the version is not pinned in a strict way.

Additionally, package managers often support adding private repositories to the package source list. In that case, both public and private repositories might be searched and the highest matching version of the package will be used.

--> If this is the case, as an attacker you can add a package with the same name but higher version to a public repository, and with some luck, it will be selected by the package manager.

# Pentesting

**Prerequisites:**
- Typically, you need to know the target package manager and its configuration.
- Knowledge of a name of a custom package not hosted publicly.
**Workflow:**
1. Search for a custom package used by the target application.
2. Create a malicious package with the same name and a fitting (newer) version.
	- Typically some code runs at install time of the package (i.e build time of the application) and during runtime of the application --> both are attack surface for code execution.
3. Publish the package to a repository used by the target.

## Python specifics

The use of the `extra-index-url` option makes a pip config vulnerable.

### Install-time Payloads

In the package definition, install-time payloads can be added in `setup.py`, e.g. by adding an installer function using the `setuptools` function `cmdclass`.

**Example setup.py:**

```python
from setuptools import setup, find_packages
from setuptools.command.install import install

class Installer(install):
      def run(self):
          install.run(self)
          with open('/tmp/code_execution_during_install', 'w') as f:
              f.write('Achieved code execution!')

setup(
    name='dummy-package',
    version='1.2.1',
    packages=find_packages(),
    classifiers=[],
    install_requires=[],
    tests_require=[],
    cmdclass={'install': Installer}
)
```

### Run-time Payloads

# Hardening
