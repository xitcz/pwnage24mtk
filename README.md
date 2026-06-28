# pwnage24mtk
Cert exploit for MTK devices.There is a logic flaw in MTK cert verification process.Similar to CVE-2023-20696.

For mtk devices,preloader verifies bl2_ext/lk/atf and then jumps to it.

These images is signed with ASN.1 certs.

But there is a logic flaw in the ASN.1 parsing process.

For old V5/V6 devices, cert content is identified by bypass_mode 1.

In this mode, any object will be stepped in.

So we can make a fake cert with 0x3(bit string) object.

The fake cert is unmodified. So it can pass the validation.

The real cert is under the fake cert.And We can put the image hash and image hdr hash at the beginning of the real cert.

For new V6 devices, cert content is identified by bypass_mode 0

In this mode, any object will be skipped except 0x30.

So we can put the image hash and image hdr hash at the beginning of the cert.

Then keep other things unmodified.

Then we can modify the image content.

So we gain EL3 control.


