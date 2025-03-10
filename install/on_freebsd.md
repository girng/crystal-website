---
layout: install
subtitle: On FreeBSD
exclude: true
permalink: /install/on_freebsd/
---

FreeBSD includes the Crystal compiler in the ports tree, starting from version FreeBSD 11.0.

Currently, it is only available for `aarch64` and `amd64` platforms.

When building Crystal code with the `--release` flag on FreeBSD, the `--no-debug` flag should be added too in order to avoid LLVM assertion errors.

## Install Package

Crystal is available as a compiled package. However, it might not be the most recent version available.


<div class="code_section">
{% highlight bash %}
sudo pkg install -y crystal shards
{% endhighlight bash %}
</div>

If you're on a `-RELEASE` version of FreeBSD, by default `pkg` is configured for the `quarterly` package set, which is updated every quarter (except for security patches, which are included ASAP).

To switch to `latest` for quicker updates, create a file `/usr/local/etc/pkg/repos/FreeBSD.conf` with the following contents:


<div class="code_section">
{% highlight ucl %}
FreeBSD: {
  url: "pkg+http://pkg.FreeBSD.org/${ABI}/latest"
}
{% endhighlight ucl %}
</div>

## Install Port

For building Crystal yourself, the required installation is available in the ports tree.

If the ports collection is not already installed, it can be downloaded using `portsnap fetch` or `git clone https://github.com/freebsd/freebsd-ports`.

<div class="code_section">
{% highlight bash %}
sudo make -C/usr/ports/lang/crystal reinstall clean
sudo make -C/usr/ports/devel/shards reinstall clean
{% endhighlight bash %}
</div>

To avoid building LLVM from source (which can take a long time), you can first install it from binary packages if you don't have it installed yet:

<div class="code_section">
{% highlight bash %}
sudo pkg install -y llvm60
{% endhighlight bash %}
</div>

Alternatively, use a smart port builder like [Synth](https://github.com/jrmarino/synth), which automatically decides to download dependencies as binary packages when there's no reason to rebuild them.
