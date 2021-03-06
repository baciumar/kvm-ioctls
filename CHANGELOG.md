# [0.6.0-2]

## Changed

- Upgrade to kvm-bindings v0.3.0-2 which enables versionize on arm.

# [0.6.0-1]

## Added

- [upstream] Support for retrieving Host_IPA_Limit for aarch64.
- [upstream] Support for parametrizable `datamatch` field
  when unregistering IO event through KVM_IOEVENTFD.
- [upstream] Support for flexible configuration of aarch64
  guest IPA size.
- [upstream] Support for `KVM_GET_DEVICE_ATTR` ioctl.
- [upstream] Support for `KVM_CAP_MSI_DEVID` ioctl.
- [upstream] Support for `KVM_CHECK_EXTENSION` ioctl.
- [upstream] Support for `KVM_GET_REG_LIST` ioctl.

# [0.5.0-2]

## Changed

- Upgrade to kvm-bindings v0.2.0-2 which uses versionize v0.1.1.

# [0.5.0-1]

Built on top of upstream rust-vmm/kvm-ioctls v0.5.0.

## Changed

- Consume 'kvm-bindings' dependency from 'github.com/firecracker-microvm'
  which provides versioned bindings for x86_64 state structs.

# v0.5.0

## Added
- Support for the vcpu ioctls `KVM_GET/SET_VCPU_EVENTS` and `KVM_GET_DIRTY_LOG`
  on `aarch64`.
- Support for the vcpu ioctl `KVM_IRQ_LINE`.

# v0.4.0

## Added
- Support for unregistering ioeventfds through `KVM_IOEVENTFD`.

## Changed
- Functions working with event FDs now require
  vmm_sys_util::eventfd::EventFd in their interface instead of
  RawFd.
- Functions working with FAM structs kvm_msr_list and kvm_msrs, were
  changed to work with their respective safe counterparts MsrList and
  respectively Msrs.
- Now exporting kvm_ioctls::Error type definition so that users of this
  crate can create their own wrapping errors without having to know the
  Error type used internally by this crate.
- No longer exporting kvm_ioctls::Result. Users of this crate should
  not have to use kvm_ioctls::Result outside the crate.
- kvm_ioctls::Error now works with errno::Error instead of io::Error.

## Removed
- CpuId safe wrapper over FAM struct kvm_cpuid2. The safe wrapper is
  now provided by the kvm_bindings crate starting with v0.2.0.
- KVM_MAX_MSR_ENTRIES and MAX_KVM_CPUID_ENTRIES. Equivalent constants
  are provided by the kvm_bindings crate starting with v0.2.0.

# v0.3.0

## Added
- Support for setting vcpu `kvm_immediate_exit` flag
- Support for the vcpu ioctl `KVM_GET_CPUID2`
- Support for the vcpu ioctl `KVM_GET_MP_STATE`
- Support for the vcpu ioctl `KVM_SET_MP_STATE`
- Support for the vcpu ioctl `KVM_GET_VCPU_EVENTS`
- Support for the vcpu ioctl `KVM_SET_VCPU_EVENTS`
- Support for the vcpu ioctl `KVM_GET_DEBUGREGS`
- Support for the vcpu ioctl `KVM_SET_DEBUGREGS`
- Support for the vcpu ioctl `KVM_GET_XSAVE`
- Support for the vcpu ioctl `KVM_SET_XSAVE`
- Support for the vcpu ioctl `KVM_GET_XCRS`
- Support for the vcpu ioctl `KVM_SET_XCRS`
- Support for the vm ioctl `KVM_GET_IRQCHIP`
- Support for the vm ioctl `KVM_SET_IRQCHIP`
- Support for the vm ioctl `KVM_GET_CLOCK`
- Support for the vm ioctl `KVM_SET_CLOCK`
- Support for the vm ioctl `KVM_GET_PIT2`
- Support for the vm ioctl `KVM_SET_PIT2`
- Support for the vcpu ioctl `KVM_GET_ONE_REG`

## Changed
- Function offering support for `KVM_SET_MSRS` also returns the number
  of MSR entries successfully written.

# v0.2.0

## Added
- Add support for `KVM_ENABLE_CAP`.
- Add support for `KVM_SIGNAL_MSI`.

## Fixed
- Fix bug in KvmRunWrapper. The memory for kvm_run struct was not unmapped
  after the KvmRunWrapper object got out of scope.
- Return proper value when receiving the EOI KVM exit.
- Mark set_user_memory_region as unsafe.

# v0.1.0

First release of the kvm-ioctls crate.

The kvm-ioctls crate provides safe wrappers over the KVM API, a set of ioctls
used for creating and configuring Virtual Machines (VMs) on Linux.
The ioctls are accessible through four structures:
- Kvm - wrappers over system ioctls
- VmFd - wrappers over VM ioctls
- VcpuFd - wrappers over vCPU ioctls
- DeviceFd - wrappers over device ioctls

The kvm-ioctls can be used on x86_64 and aarch64. Right now the aarch64
support is considered experimental.
