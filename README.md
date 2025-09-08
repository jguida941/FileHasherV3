# 📁 File Monitor & Hasher - Professional Documentation
### Advanced Real-Time File Integrity Monitoring System

**Version:** 2.0 (Work In Progress)  
**Status:** 🚧 Development Phase - Critical Issues Pending  
**Architecture:** Partially Modularized PyQt6 Application  
**Code Base:** ~10,000+ Lines | 10 Professional Themes | Plugin System  

---

## 🎯 Executive Summary

The **File Monitor & Hasher** is a sophisticated PyQt6-based desktop application designed for real-time file and directory integrity monitoring using cryptographic hash algorithms. While feature-rich with 10 professional themes and advanced capabilities, the application is currently in a **work-in-progress state** with several critical issues that need resolution before production deployment.

### ✅ Core Features (Working)
- **Multi-Algorithm Hashing:** SHA-256, SHA3-256, BLAKE2b support
- **Real-Time Monitoring:** QFileSystemWatcher-based change detection
- **Professional Theming:** 10 distinct scientific/professional themes
- **Plugin Architecture:** Webhook notifications, security auditing
- **Data Visualization:** Real-time charts using PyQtGraph
- **History Database:** SQLite-based change tracking with annotations
- **Export Capabilities:** CSV, JSON, encrypted ZIP archives

### ⚠️ Known Issues (Work In Progress)
- **Table Row Highlighting:** Alternating row colors broken across themes
- **Monolithic Codebase:** Main file still 6,266 lines (partial modularization)
- **Chart Statistics:** Incorrect file count display
- **Theme Consistency:** CSS application gaps in some components
- **Performance:** UI freezes during large file operations

---

## 🏗️ System Architecture

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                      File Monitor & Hasher                      │
│                         PyQt6 Application                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │   UI Layer   │  │  Core Logic  │  │   Plugins    │           │
│  │              │  │              │  │              │           │
│  │ ┌──────────┐ │  │ ┌──────────┐ │  │ ┌──────────┐ │           │
│  │ │MainWindow│ │  │ │HashMonitor │  │ │  Webhook │ │           │
│  │ └──────────┘ │  │ └──────────┘ │  │ └──────────┘ │           │
│  │ ┌──────────┐ │  │ ┌──────────┐ │  │ ┌──────────┐ │           │
│  │ │  Tabs    │ │  │ │HashCompute │  │ │ Security │ │           │
│  │ └──────────┘ │  │ └──────────┘ │  │ └──────────┘ │           │
│  │ ┌──────────┐ │  │ ┌──────────┐ │  │              │           │
│  │ │ Widgets  │ │  │ │ Database │ │  │              │           │
│  │ └──────────┘ │  │ └──────────┘ │  │              │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │Theme Manager │  │File Watcher  │  │   Utilities  │           │
│  │              │  │              │  │              │           │
│  │ 10 Themes    │  │ QFileSystem  │  │   Export     │           │
│  │ QSS Engine   │  │   Watcher    │  │   Import     │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   External Systems  │
                    ├─────────────────────┤
                    │ • File System       │
                    │ • SQLite Database   │
                    │ • Webhook Endpoints │
                    │ • Log Files         │
                    └─────────────────────┘
```

### Data Flow Diagram

```
┌──────────────┐     File Selection     ┌──────────────┐
│     User     │ ──────────────────────▶│   UI Layer   │
└──────────────┘                        └──────────────┘
                                                │
                                                ▼
                                        ┌──────────────┐
                                        │ Hash Monitor │
                                        └──────────────┘
                                                │
                              ┌─────────────────┼─────────────────┐
                              ▼                 ▼                 ▼
                      ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
                      │File Watcher  │ │Hash Computer │ │   Database   │
                      └──────────────┘ └──────────────┘ └──────────────┘
                              │                 │                 │
                              ▼                 ▼                 ▼
                      ┌──────────────────────────────────────────┐
                      │            Event Processing              │
                      │  • File Changes Detected                 │
                      │  • Hash Values Computed                  │
                      │  • History Entries Stored                │
                      └──────────────────────────────────────────┘
                                                │
                                                ▼
                      ┌──────────────────────────────────────────┐
                      │             Plugin System                │
                      │  • Webhook Notifications                 │
                      │  • Security Audit Logs                   │
                      │  • Custom Event Handl  rs                │
                      └──────────────────────────────────────────┘
                                                │
                                                ▼
                      ┌──────────────────────────────────────────┐
                      │          UI Update & Display             │
                      │  • History Table Updated                 │
                      │  • Charts Refreshed                      │
                      │  • Status Indicators Changed             │
                      └──────────────────────────────────────────┘
```

### Threading Model

```
┌─────────────────────────────────────────────────────────────┐
│                      Main UI Thread                         │
│  • PyQt6 Event Loop                                         │
│  • User Interface Updates                                   │
│  • Theme Application                                        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ├──────────────┐
                              ▼              ▼
┌──────────────────────┐  ┌──────────────────────┐
│  HashMonitor Thread  │  │  Plugin Threads      │
│  • File Monitoring   │  │  • Webhook Posts     │
│  • Hash Computation  │  │  • Audit Logging     │
│  • Change Detection  │  │  • Custom Plugins    │
└──────────────────────┘  └──────────────────────┘
         │                           │
         └───────────┬───────────────┘
                     ▼
         ┌──────────────────────┐
         │   Signal/Slot IPC    │
         │  • Thread-safe comm  │
         │  • Event emission    │
         └──────────────────────┘
```

---

## 📂 Complete File Tree Structure

```
FixedFileHasherV3/
│
├── 📄 main.py                          # Application entry point
├── 📄 file_hasher.py                   # LEGACY: Monolithic main file (6,266 lines)
│
├── 📁 core/                            # Core business logic (modularized)
│   ├── __init__.py                     # Package initialization
│   ├── hash_monitor.py                 # Hash monitoring thread & computation
│   └── database.py                     # SQLite history database operations
│
├── 📁 ui/                              # User interface components
│   ├── __init__.py                     # UI package exports
│   ├── main_window.py                  # Main application window
│   ├── component_styler.py             # Component styling utilities
│   ├── enhanced_developer_tools.py     # Developer tools & theme editor
│   │
│   ├── 📁 theme_studio/                # Theme editing subsystem
│   │   ├── __init__.py
│   │   ├── theme_editor.py             # Live theme editor interface
│   │   └── qss_generator.py            # QSS stylesheet generator
│   │
│   └── 📁 widgets/                     # Custom UI widgets
│       ├── __init__.py
│       └── status_chart.py             # Real-time monitoring chart
│
├── 📁 themes/                          # Theme system
│   ├── __init__.py
│   └── theme_definitions.py            # 10 theme configurations (29,788 lines)
│
├── 📁 stylesheets/                     # Generated QSS files
│   ├── *.qss (10 files)                # One per theme
│   └── 📁 metadata/                    # Theme metadata JSON files
│       └── *.json (10 files)
│
├── 📁 tests/                           # Test suite
│   ├── test_phase1_themes.py           # Phase 1: Basic theme tests
│   ├── test_phase2_*.py                # Phase 2: Comprehensive tests
│   ├── test_phase3_*.py                # Phase 3: Refactoring tests
│   ├── test_phase10_*.py               # Phase 10: Integration tests
│   ├── test_critical_fixes.py          # Critical bug fix tests
│   └── test_comprehensive_qa.py        # Full QA test suite
│
├── 📁 exported_themes/                 # Theme export directory
│   ├── *.theme.json (10 files)         # Individual theme exports
│   └── complete_theme_bundle.json      # All themes bundle
│
├── 📁 md_archive/                      # Documentation archive
│   ├── master.md                       # Original requirements
│   ├── README.md                       # Original documentation
│   ├── PHASE2_COMPLETE_REPORT.md       # Development reports
│   └── *.md (various)                  # Planning documents
│
├── 📁 docs/                            # Current documentation
│   └── THEME_PREVIEW.md                # Theme preview documentation
│
├── 📁 theme_screenshots/               # Theme preview images
│   └── *.png (70+ screenshots)
│
├── 📄 Support Files:
│   ├── comprehensive_fix_and_test.py   # Fix validation script
│   ├── systematic_unit_test_framework.py # Test framework
│   ├── export_themes.py                # Theme export utility
│   ├── capture_screenshots.py          # Screenshot generation
│   ├── professional_styling_enhancer.py # Style enhancement tools
│   └── fix_css_compatibility.py        # CSS compatibility fixes
│
└── 📄 Documentation Files:
    ├── CURRENT_ISSUES_ANALYSIS.md      # Current issues documentation
    ├── REFACTORING_CHECKLIST.md        # Refactoring guide
    ├── UNIVERSAL_PROJECT_PLAN.md       # Project roadmap
    └── PHASE_10_COMPLETE_*.md          # Phase completion reports
```

---

## 🚧 Current Development Status

### ✅ **COMPLETED FEATURES**

| Component | Status | Description |
|-----------|--------|-------------|
| **Core Hashing** | ✅ Working | SHA-256, SHA3-256, BLAKE2b algorithms |
| **File Monitoring** | ✅ Working | Real-time change detection via QFileSystemWatcher |
| **Database** | ✅ Working | SQLite history with annotations |
| **Basic UI** | ✅ Working | 6 tabs, all basic controls functional |
| **Theme Engine** | ✅ Partial | 10 themes load but have consistency issues |
| **Plugin System** | ✅ Working | Webhook & security audit plugins functional |
| **Export System** | ✅ Working | CSV, JSON, ZIP export capabilities |
| **Charts** | ⚠️ Buggy | Display works but statistics incorrect |

### ❌ **WORK IN PROGRESS / BROKEN**

| Issue | Severity | Description | Impact |
|-------|----------|-------------|--------|
| **Table Row Highlighting** | 🔴 Critical | Alternating row colors not visible in most themes | Professional appearance compromised |
| **Monolithic Architecture** | 🔴 Critical | Main file still 6,266 lines despite partial modularization | Maintenance nightmare |
| **Chart Statistics** | 🟡 Major | Shows "100 files" when monitoring 1 file | Misleading information |
| **Theme Consistency** | 🟡 Major | Some widgets don't receive theme styles | Inconsistent appearance |
| **Performance Issues** | 🟡 Major | UI freezes on large file operations | Poor user experience |
| **CSS Compatibility** | 🟠 Minor | Unsupported properties in themes | Console warnings |
| **Documentation** | 🟠 Minor | Incomplete user manual | User confusion |

---

## 📋 TODO List (Priority Order)

### 🔴 **CRITICAL - Must Fix Immediately**

```markdown
□ 1. Fix table row alternating colors across all 10 themes
    - [ ] Standardize QTableWidget::item:alternate CSS
    - [ ] Ensure minimum contrast ratio of 3:1 (WCAG AA)
    - [ ] Test each theme systematically
    - [ ] Add visual regression tests

□ 2. Complete modularization of file_hasher.py
    - [ ] Extract remaining components to ui/tabs/
    - [ ] Move plugin system to plugins/ module  
    - [ ] Separate theme logic into themes/manager.py
    - [ ] Remove duplicate code between modules

□ 3. Fix chart statistics accuracy
    - [ ] Correct file count display logic
    - [ ] Differentiate data points vs actual files
    - [ ] Add proper scaling for large numbers
    - [ ] Fix "Files Monitored: 100" bug
```

### 🟡 **HIGH PRIORITY - Core Functionality**

```markdown
□ 4. Improve theme application consistency
    - [ ] Ensure all widgets receive theme updates
    - [ ] Fix QScrollBar, QProgressBar styling gaps
    - [ ] Add theme validation before application
    - [ ] Create theme testing framework

□ 5. Resolve performance issues
    - [ ] Move hash computation to separate thread pool
    - [ ] Implement progress indicators for long operations
    - [ ] Add operation cancellation support
    - [ ] Optimize database queries with pagination

□ 6. Enhance error handling
    - [ ] Add user-friendly error messages
    - [ ] Implement retry logic for transient failures
    - [ ] Add comprehensive logging throughout
    - [ ] Create error recovery mechanisms
```

### 🟠 **MEDIUM PRIORITY - Polish & Features**

```markdown
□ 7. Complete plugin system enhancements
    - [ ] Add plugin configuration UI
    - [ ] Implement plugin marketplace concept
    - [ ] Add more plugin hooks/events
    - [ ] Create plugin development SDK

□ 8. Improve export functionality
    - [ ] Add batch export operations
    - [ ] Implement scheduled exports
    - [ ] Add cloud storage integration
    - [ ] Create report templates

□ 9. Add accessibility features
    - [ ] Implement keyboard navigation
    - [ ] Add screen reader support
    - [ ] Create high contrast mode
    - [ ] Add tooltips everywhere
```

### 🟢 **LOW PRIORITY - Nice to Have**

```markdown
□ 10. Documentation & training
    - [ ] Create video tutorials
    - [ ] Write API documentation
    - [ ] Add interactive help system
    - [ ] Create theme creation guide

□ 11. Advanced features
    - [ ] Add file recovery capabilities
    - [ ] Implement blockchain verification
    - [ ] Add network monitoring mode
    - [ ] Create mobile companion app

□ 12. Testing & QA
    - [ ] Achieve 80% code coverage
    - [ ] Add integration test suite
    - [ ] Create performance benchmarks
    - [ ] Implement continuous integration
```

---

## 🛠️ Installation & Setup

### Prerequisites
```bash
# Python 3.8+ required
python --version

# Install required packages
pip install PyQt6 pyqtgraph numpy
```

### Installation Steps
```bash
# Clone repository
git clone [repository-url]
cd FixedFileHasherV3

# Install dependencies
pip install -r requirements.txt  # Note: requirements.txt needs to be created

# Run application
python main.py
```

### First Run Issues
- **Missing PyQtGraph:** Charts will be disabled if not installed
- **Theme Loading:** Initial theme load may be slow
- **Database Creation:** First run creates ~/.file_monitor/ directory

---

## 📊 Theme System Documentation

### Available Themes (10 Professional Themes)

| Theme Name | Style | Primary Colors | Use Case |
|------------|-------|----------------|----------|
| **dark_scientist** | Modern Dark | Cyan/Purple gradients | Data analysis |
| **arctic_laboratory** | Clean Light | Blue/White | Medical/Clinical |
| **neon_research** | Vibrant Dark | Neon Purple/Pink | Creative work |
| **medical_professional** | Clinical | Teal/White | Healthcare |
| **space_mission** | Space Dark | Orange/Dark Blue | Aerospace |
| **high_contrast** | Accessibility | Yellow/Black | Vision impaired |
| **ocean_laboratory** | Marine | Blue/Aqua | Marine research |
| **forest_research** | Natural | Green/Brown | Environmental |
| **industrial_monitor** | Industrial | Gray/Orange | Manufacturing |
| **quantum_computing** | Tech Dark | Purple/Cyan | Tech/Computing |

### Theme Architecture Issues

```python
# Current problematic implementation in themes/theme_definitions.py
THEMES = {
    "theme_name": {
        "colors": {...},           # Color definitions
        "fonts": {...},            # Typography settings
        "component_styles": {...},  # Component-specific styles
        "table_styles": {
            "alt_row": "color",    # ⚠️ BROKEN - Not applying correctly
            "hover": "color",      # ⚠️ INCONSISTENT across themes
        }
    }
}
```

---

## 🔌 Plugin System Architecture

### Plugin Base Class
```python
class PluginBase(ABC):
    @abstractmethod
    def on_hash_computed(self, path, hash_value, algorithm, changed, timestamp):
        """Called when hash is computed"""
        pass
    
    @abstractmethod
    def on_change_detected(self, path, event_type, timestamp):
        """Called when file change detected"""
        pass
```

### Available Plugins
1. **WebhookPlugin:** Sends HTTP notifications on events
2. **SecurityAuditPlugin:** Logs security-relevant events
3. **Custom plugins:** Can be added via plugin system

---

## 🧪 Testing Strategy

### Current Test Coverage
```
Tests Run: 85
Passed: 62 (73%)
Failed: 23 (27%)
Coverage: ~45% (estimated)
```

### Test Categories
- **Unit Tests:** Individual component testing
- **Integration Tests:** Module interaction testing
- **Theme Tests:** Visual consistency validation
- **Performance Tests:** Load and stress testing

### Running Tests
```bash
# Run all tests
python -m pytest tests/

# Run specific test suite
python tests/test_phase10_complete_integration.py

# Run with coverage
pytest --cov=. tests/
```

---

## 📈 Performance Metrics

### Current Performance Issues
| Operation | Current | Target | Status |
|-----------|---------|--------|--------|
| File Hash (1MB) | 50ms | 20ms | ⚠️ Needs optimization |
| Theme Switch | 800ms | 200ms | ❌ Too slow |
| Chart Update | 1000ms | 100ms | ❌ Excessive CPU usage |
| Database Query (1000 rows) | 500ms | 50ms | ⚠️ No pagination |

---

## 🚀 Development Roadmap

### Phase 1: Critical Fixes (Current)
- Fix table row highlighting
- Complete modularization
- Resolve performance issues

### Phase 2: Stabilization (Next 2 weeks)
- Comprehensive testing
- Bug fixes
- Documentation

### Phase 3: Enhancement (Next month)
- New features
- UI/UX improvements
- Advanced plugins

### Phase 4: Production Ready (2 months)
- Security audit
- Performance optimization
- Deployment packages

---

## 🤝 Contributing

### Development Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate  # Windows

# Install dev dependencies
pip install -r requirements-dev.txt  # Needs creation

# Run tests before committing
pytest tests/
```

### Code Style Guidelines
- Follow PEP 8
- Use type hints
- Document all functions
- Write tests for new features

---

## 📝 License

This project is licensed under the Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0).

You are free to:
- Share — copy and redistribute the material in any medium or format
- Adapt — remix, transform, and build upon the material

Under the following terms:
- **Attribution** — You must give appropriate credit.
- **NonCommercial** — You may not use the material for commercial purposes.

See the [LICENSE](LICENSE) file for full details.
---

## ⚠️ Disclaimers

**This application is currently in active development and should NOT be used in production environments.**

### Known Limitations:
- UI may freeze during large file operations
- Some themes have visual inconsistencies
- Chart statistics are inaccurate
- Memory usage not optimized
- No multi-language support

### Security Considerations:
- Hash algorithms are cryptographic but not for security
- No encryption for local database
- Webhook endpoints not authenticated
- No input sanitization in some areas

---

## 📞 Support & Contact

- **Issues:** Report bugs via GitHub Issues
- **Documentation:** See /docs directory
- **Development Status:** Check CURRENT_ISSUES_ANALYSIS.md

---

## 🙏 Acknowledgments

- PyQt6 for the GUI framework
- PyQtGraph for real-time charting
- SQLite for database functionality
- Community contributors and testers

---

*Last Updated: 2025-09-07*  
*Version: 2.0-dev*  
*Status: Work In Progress - Not Production Ready*
