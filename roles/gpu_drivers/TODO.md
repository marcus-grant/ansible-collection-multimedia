# TODO: gpu_drivers Role

This role manages GPU driver installation and configuration for AMD, Intel, and NVIDIA graphics hardware.

## Atomic TDD Specifications

### 1. GPU Hardware Detection

#### 1.1 Detect GPU Vendor
- [ ] **Test:** Verify AMD GPU detection from lspci output
- [ ] **Test:** Verify Intel GPU detection from lspci output  
- [ ] **Test:** Verify NVIDIA GPU detection from lspci output
- [ ] **Test:** Handle missing lspci command gracefully
- [ ] **Test:** Return empty list when no GPUs found
- [ ] **Implementation:** Parse lspci output for GPU vendor IDs

#### 1.2 Identify GPU Model
- [ ] **Test:** Extract AMD GPU model name from device info
- [ ] **Test:** Extract Intel GPU generation from device info
- [ ] **Test:** Extract NVIDIA GPU series from device info
- [ ] **Test:** Handle unknown/unsupported GPU models
- [ ] **Implementation:** Map PCI IDs to human-readable names

#### 1.3 Multiple GPU Support
- [ ] **Test:** Detect all GPUs in multi-GPU systems
- [ ] **Test:** Identify primary GPU for display
- [ ] **Test:** Handle hybrid graphics (Intel+NVIDIA)
- [ ] **Test:** Handle hybrid graphics (AMD+AMD)
- [ ] **Implementation:** Create GPU inventory with priorities

### 2. Distribution Detection

#### 2.1 Identify Distribution
- [ ] **Test:** Detect Ubuntu and version
- [ ] **Test:** Detect Debian and version
- [ ] **Test:** Detect Fedora and version
- [ ] **Test:** Detect Arch Linux
- [ ] **Test:** Fail gracefully on unsupported distributions
- [ ] **Implementation:** Use ansible_facts for distribution info

#### 2.2 Package Manager Setup
- [ ] **Test:** Identify correct package manager for distribution
- [ ] **Test:** Verify repository management commands
- [ ] **Test:** Handle package manager lock files
- [ ] **Implementation:** Abstract package operations by distro

### 3. AMD GPU Driver Installation

#### 3.1 Mesa Driver Setup
- [ ] **Test:** Check if Mesa drivers already installed
- [ ] **Test:** Install Mesa drivers on Ubuntu/Debian
- [ ] **Test:** Install Mesa drivers on Fedora
- [ ] **Test:** Install Mesa drivers on Arch
- [ ] **Test:** Verify driver version meets minimum requirements
- [ ] **Implementation:** Distribution-specific Mesa packages

#### 3.2 AMD Firmware Installation
- [ ] **Test:** Check for required AMD firmware packages
- [ ] **Test:** Install firmware for specific GPU models
- [ ] **Test:** Handle firmware package conflicts
- [ ] **Implementation:** Model-specific firmware selection

#### 3.3 AMDGPU Configuration
- [ ] **Test:** Create AMDGPU config if missing
- [ ] **Test:** Enable required kernel modules
- [ ] **Test:** Configure display manager integration
- [ ] **Test:** Set appropriate DRI permissions
- [ ] **Implementation:** System configuration templates

### 4. Intel GPU Driver Installation

#### 4.1 Intel Graphics Driver
- [ ] **Test:** Check Intel driver installation status
- [ ] **Test:** Install i915 driver dependencies
- [ ] **Test:** Handle legacy Intel GPUs (i810, i915)
- [ ] **Test:** Install Intel media driver (iHD)
- [ ] **Implementation:** Generation-based driver selection

#### 4.2 Intel Firmware Setup
- [ ] **Test:** Detect required GuC/HuC firmware
- [ ] **Test:** Install generation-specific firmware
- [ ] **Test:** Verify firmware loading in dmesg
- [ ] **Implementation:** Firmware package management

### 5. NVIDIA Driver Installation

#### 5.1 Driver Version Selection
- [ ] **Test:** Determine compatible driver for GPU model
- [ ] **Test:** Handle legacy NVIDIA GPUs
- [ ] **Test:** Respect user-specified driver version
- [ ] **Test:** Validate driver version format
- [ ] **Implementation:** GPU model to driver mapping

#### 5.2 NVIDIA Repository Setup
- [ ] **Test:** Add NVIDIA repository on Ubuntu
- [ ] **Test:** Configure RPM Fusion on Fedora
- [ ] **Test:** Handle NVIDIA AUR packages on Arch
- [ ] **Test:** Verify repository GPG keys
- [ ] **Implementation:** Distribution-specific repos

#### 5.3 Proprietary Driver Installation
- [ ] **Test:** Remove nouveau if present
- [ ] **Test:** Install NVIDIA driver packages
- [ ] **Test:** Handle kernel module compilation
- [ ] **Test:** Configure NVIDIA persistence daemon
- [ ] **Test:** Set up NVIDIA settings tool
- [ ] **Implementation:** Complete NVIDIA stack

### 6. Vulkan Support

#### 6.1 Vulkan Runtime Installation
- [ ] **Test:** Install Vulkan loader libraries
- [ ] **Test:** Install Vulkan validation layers
- [ ] **Test:** Install vendor-specific Vulkan drivers
- [ ] **Test:** Handle missing Vulkan packages gracefully
- [ ] **Implementation:** Vulkan package dependencies

#### 6.2 Vulkan ICD Configuration
- [ ] **Test:** Configure AMD Vulkan ICD
- [ ] **Test:** Configure Intel Vulkan ICD
- [ ] **Test:** Configure NVIDIA Vulkan ICD
- [ ] **Test:** Verify ICD JSON files exist
- [ ] **Implementation:** ICD file management

#### 6.3 Vulkan Validation
- [ ] **Test:** Run vulkaninfo successfully
- [ ] **Test:** Detect Vulkan device capabilities
- [ ] **Test:** Handle Vulkan initialization errors
- [ ] **Implementation:** Vulkan functionality tests

### 7. System Integration

#### 7.1 User Group Configuration
- [ ] **Test:** Add users to video group
- [ ] **Test:** Add users to render group (if exists)
- [ ] **Test:** Handle missing groups gracefully
- [ ] **Test:** Preserve existing group memberships
- [ ] **Implementation:** Group management tasks

#### 7.2 Display Manager Integration
- [ ] **Test:** Configure GDM for NVIDIA
- [ ] **Test:** Configure SDDM for all GPUs
- [ ] **Test:** Configure LightDM settings
- [ ] **Test:** Handle missing display managers
- [ ] **Implementation:** Display manager templates

#### 7.3 Boot Configuration
- [ ] **Test:** Update initramfs after driver changes
- [ ] **Test:** Configure GRUB for NVIDIA
- [ ] **Test:** Handle systemd-boot configurations
- [ ] **Test:** Verify boot parameters applied
- [ ] **Implementation:** Bootloader management

### 8. Validation and Testing

#### 8.1 Driver Verification
- [ ] **Test:** Verify kernel modules loaded
- [ ] **Test:** Check OpenGL rendering string
- [ ] **Test:** Validate DRI device permissions
- [ ] **Test:** Test basic 3D acceleration
- [ ] **Implementation:** Runtime validation tasks

#### 8.2 Error Handling
- [ ] **Test:** Rollback on installation failure
- [ ] **Test:** Log detailed error messages
- [ ] **Test:** Provide troubleshooting guidance
- [ ] **Test:** Handle partial installations
- [ ] **Implementation:** Error recovery procedures

## Testing Order

1. Start with distribution detection (foundation for everything)
2. Implement GPU hardware detection (determines driver choice)
3. Add AMD driver support (most straightforward)
4. Add Intel driver support (similar to AMD)
5. Implement NVIDIA support (most complex)
6. Add Vulkan configuration (cross-vendor)
7. Complete system integration (ties everything together)
8. Implement validation and error handling (ensures reliability)

## Dependencies

- `lspci` command (pciutils package)
- Distribution package managers (apt, dnf, pacman)
- Python 3.x for complex parsing tasks
- Ansible 2.9+ for role functionality