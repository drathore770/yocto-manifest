# Yocto OSS Manifest README
This repo downloads manifests for Yocto OSS layers.
Note that this does not include the Yocto Project's Poky repository. Instead, the import pieces that go into the Poky repository are includedfrom their upstream git repositories directly (e.g. oe-core, bitbake, etc).

# Setup Scarthgap Yocto source
	$ export PATH=~/bin:/bin:/usr/bin:/usr/sbin:/sbin:/usr/cisco/bin
	$ repo init -u https://github.com/drathore770/yocto-manifest.git -b scarthgap
	$ repo sync
	$ source source/openembedded-core/oe-init-build-env build
	$ bitbake core-image-minimal

# Enabling CVE check:
The Yocto Project provides a cve-check class which can be enabled to scan packages for public CVE’s. You can use this feature to scan individual packages but also on images (which will scan all packages included in that specific image).

It utilizes the NATIONAL VULNERABILITY DATABASE, from which it performs the lookup.

To enable the CVE check you can add the following configuration to conf/local.conf:

	INHERIT += "cve-check"

Once this is enabled you can run CVE checks on individual package(s):

	$ bitbake -c cve_check <package/image name>
 
# Example:
	$ bitbake -c cve_check openssl
	$ bitbake core-image-sato
	$ bitbake -k -c cve_check universe
