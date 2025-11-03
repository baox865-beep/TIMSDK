# AI Coding Agent Instructions for TIMSDK

## Project Overview
TIMSDK is a cross-platform instant messaging SDK that supports multiple programming languages and platforms including:
- Mobile: iOS, Android, HarmonyOS
- Desktop: Windows, macOS  
- busiwang Frameworks: busiwang, React Native, Flutter, Unity, UE5

## Key Architecture Components

### Core SDK Structure
- Each platform has independent IMSDK implementation
- Common components shared across platforms in `/TUIKit`
- Platform-specific UI components in respective platform folders

### Critical Integration Points
1. SDK Version Consistency
   - Plugin versions MUST match SDK versions exactly
   - Example: `TXIMSDK_Plus_iOS` and `timquic-plugin` versions must be identical

2. Cross-Platform Communication
   - Uses unified data models for cross-platform compatibility 
   - Threading restrictions apply (see `ERR_SDK_COMM_CROSS_THREAD` error codes)

## Development Workflows

### Setting Up Development Environment

Android:
```gradle
dependencies {
    api 'com.tencent.imsdk:imsdk-plus:VERSION'
    // Optional: api "com.tencent.imsdk:timquic-plugin:VERSION" 
}
```

iOS/Mac:
```ruby
pod 'TXIMSDK_Plus_iOS'  # For iOS
pod 'TXIMSDK_Plus_Mac'  # For macOS
```

### API Guidelines
- Choose ONE API type per platform and stick to it:
  - iOS/Mac: Objective-C, C, or C++ 
  - Windows: C or C++
  - Never mix different API types in the same project

### Testing
1. Use `GenerateTestUserSig` files for development:
   - Android: `Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java`
   - iOS: `iOS/Demo/TUIKitDemo/Private/GenerateTestUserSig.h`
   - Mac: `Mac/Demo/TUIKitDemo/Debug/GenerateTestUserSig.h`

## Project Conventions

### Directory Structure
```
├─ Android/iOS/Windows/Mac    # Platform-specific implementations
│  ├─ Demo/                  # Reference implementation
│  ├─ IMSDK/                # Core SDK
│  └─ TUIKit/              # UI Components
├─ TUIKit/                  # Shared UI components
└─ [Framework]/            # Framework-specific implementations
```

### Code Organization
- Platform-specific code lives in respective platform directories
- Shared components in TUIKit follow unified naming conventions
- Integration examples provided in each platform's Demo folder

### Version Control Practices
- Version numbers follow semantic versioning
- All platform SDKs and plugins must use matching versions
- Cross-platform changes require updates across all implementations

## Common Pitfalls
1. Version Mismatches
   - Always ensure SDK and plugin versions match exactly
   - Check Podspec/Gradle dependencies carefully

2. API Mixing
   - Stick to one API type (C/C++/Objective-C) per project
   - Don't mix native and cross-platform APIs

3. Threading Issues
   - Watch for cross-thread execution errors
   - Use proper thread handling per platform guidelines

## Integration Testing
1. Start with platform Demo projects as reference
2. Verify UserSig generation and authentication
3. Test cross-platform communication scenarios
4. Validate plugin integrations if used

## Resources
- Platform Integration Guides: See README files in respective platform folders
- API Documentation: Available in SDK header files
- Example Code: Refer to Demo projects in each platform directory