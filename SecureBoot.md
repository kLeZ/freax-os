# Introduction #

We want to let the users use SecureBoot as we think that this can be a security enhancement in some ways, but we don't want to trust Microsoft for doing security-related things, because we know that Microsoft isn't able to do any security-related thing at all.

So we needed to find a way to implement SecureBoot support on our distribution.
We thought to use Garrett's Shim, a pre-bootloader that can run trustfully into SecureBoot and load a normal bootloader such as Grub2-efi.

Some details on how to build Shim with a self-signed key and replace Microsoft's ones is placed [here](http://www.rodsbooks.com/efi-bootloaders/secureboot.html).
The Shim source code is hosted by Garrett on GitHub, and is available [here](https://github.com/mjg59/shim).

# Details #

Based on the informations we found, there's no way to install extra keys on SecureBoot without user intervention directly on the UEFI firmware and unfortunately there's not even a common way to do so, assumed that our firmware _has_ a way to install such keys. We think that this will be a geeky thing that a normal user usually does not do then the [binary](http://www.codon.org.uk/~mjg59/shim-signed/) we're going to use is already signed with a Microsoft's key by Matt Garrett, ex RedHat employee and deeply involved in the fedora community where he firstly released his shim program. This binary is the same you can find on fedora, while Canonical and Novell decided to buy their own keys so they can easily sign new binaries without third parties intervention. We, as a little os developers with such a 0-day community, cannot let ourselves to buy a key from Microsoft, so we apologize right now for using Microsoft's keys (that means that we and you have to trust MS in some way), bought by others, with a binary not built by us and not signed by you (the only person you can trust, in this information era in which people can be very bad even if we try to trust them).

Our hint is, if you are a geeky person or simply you know _exactly_ what you're doing, recompile the shim thing, sign it with your own keys and install those keys in you UEFI firmware, literally **pissing off** Microsoft's ones.