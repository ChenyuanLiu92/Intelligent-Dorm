# I-Dorm-Guard: A Intelligent Dorm System 🏠🔐

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.0+-red.svg)](https://opencv.org/)
[![ArcFace](https://img.shields.io/badge/ArcFace-Engine-orange.svg)](https://www.arcsoft.com.cn/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An intelligent dormitory security system based on facial recognition technology, providing modern solutions for dormitory safety management.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### 🎯 Core Functions
- **Real-time Face Recognition Monitoring** - High-precision face recognition based on ArcFace engine
- **Smart Access Control** - Automatic recognition of authorized personnel, denying stranger access
- **Multi-room Monitoring** - Unified management of multiple dormitory rooms
- **Web Management Interface** - Modern web interface supporting real-time monitoring and data management

### 🔧 Management Functions
- **User Management** - Student information registration and permission management
- **Room Management** - Dormitory room allocation and configuration
- **Notification System** - Real-time notifications for abnormal situations
- **Data Analytics** - Access records, security statistics and data analysis

### 🔒 Security Features
- **High Accuracy Recognition** - Recognition similarity threshold up to 88%
- **Liveness Detection** - Prevents photo spoofing attacks
- **24/7 Monitoring** - Continuous monitoring
- **Intrusion Alerts** - Automatic alerts for unauthorized access

## 🏗️ Tech Stack

### Backend
- **Web Framework**: Flask 2.0+
- **Database**: MySQL + SQLAlchemy ORM
- **Face Recognition**: ArcFace SDK
- **Computer Vision**: OpenCV
- **Language**: Python 3.7+

### Frontend
- **UI Framework**: Bootstrap
- **Charts**: jqPlot
- **Styling**: CSS3 + Font Awesome
- **Responsive Design**: Multi-device support

### System Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Camera Module │    │  ArcFace Engine │    │  Web Interface  │
│   摄像头模块     │───▶│  人脸识别引擎   │───▶│   Web管理界面   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Video Stream   │    │ Feature Extract │    │ User Management │
│   视频流处理     │    │   特征提取比对   │    │   用户权限管理   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🚀 Installation

### Requirements
- Python 3.7+
- MySQL 5.7+
- Camera device
- ArcFace SDK license

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/i-dorm-guard.git
cd i-dorm-guard
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Database Configuration
```bash
# Create database
mysql -u root -p
CREATE DATABASE dormguard CHARACTER SET utf8;

# Configure database connection in app.py
SQLALCHEMY_DATABASE_URI = 'mysql://root:password@localhost:3306/dormguard?charset=utf8'
```

### 4. ArcFace SDK Configuration
- Apply for ArcFace SDK license
- Place license file in project root directory
- Configure APPID and SDKKey in `demo_cam.py`

### 5. Run Application
```bash
python app.py
```

Visit `http://localhost:5000` to access the system.

## 📖 Usage

### Basic Workflow

1. **System Login**
   - Access web interface
   - Login with administrator account

2. **User Management**
   - Add student information
   - Upload face photos to `asserts/` directory
   - Assign room permissions

3. **Start Monitoring**
   ```python
   from demo_cam import start_monitoring
   start_monitoring()
   ```

4. **Real-time Monitoring**
   - View live monitoring feed
   - Monitor recognition results and alerts

### Advanced Configuration

#### Face Recognition Parameter Tuning
```python
# Key parameters in demo_cam.py
definite_thres = 0.88  # Definite threshold, recommended 0.85-0.9
threshold = 0.7        # Recognition threshold, recommended 0.6-0.8
```

#### Camera Configuration
```python
# Local camera
cap = cv2.VideoCapture(0)

# Network camera
cap = cv2.VideoCapture("http://192.168.1.100:8081/")
```

## 📚 API Documentation

### User Management API
```python
# User login verification
POST /login
{
    "id": "student_id",
    "password": "password"
}

# User registration
POST /register
{
    "id": "student_id",
    "username": "name",
    "password": "password"
}
```

### Room Management API
```python
# Room information query
GET /room/<room_id>

# WeChat Mini Program interface
GET /room/wec
```

### Monitoring Interface
```python
# Real-time monitoring page
GET /video

# Notification panel
GET /notice_board
```

## 📁 Project Structure

```
i-dorm-guard/
├── app.py                 # Flask application main file
├── demo_cam.py           # Face recognition monitoring module
├── ArcFace64.dat         # ArcFace license file
├── requirements.txt      # Dependencies list
├── LICENSE              # Open source license
├── README.md           # Project documentation
│
├── arcface/            # ArcFace engine wrapper
│   ├── engine.py      # Face recognition engine
│   ├── lib_func.py    # Low-level function wrapper
│   └── struct_info.py # Data structure definitions
│
├── controller/         # Web controllers
│   ├── index.py       # Home controller
│   ├── user.py        # User management
│   ├── room.py        # Room management
│   ├── video.py       # Video monitoring
│   └── notice.py      # Notification system
│
├── moudle/            # Data models
│   ├── users.py       # User data model
│   └── rooms.py       # Room data model
│
├── common/            # Common modules
│   ├── database.py    # Database connection
│   └── utility.py     # Utility functions
│
├── templates/         # HTML templates
│   ├── base.html      # Base template
│   ├── login.html     # Login page
│   ├── monitor.html   # Monitoring interface
│   └── ...
│
├── static/           # Static resources
│   ├── css/         # Style files
│   ├── js/          # JavaScript files
│   ├── img/         # Image resources
│   └── ...
│
├── asserts/         # Face image library
│   ├── student1.jpg
│   ├── student2.jpg
│   └── ...
│
└── lib/            # Third-party library files
    ├── libarcsoft_face_engine.dll
    └── ...
```

## 🤝 Contributing

We welcome contributions of any kind! Please follow these steps:

1. **Fork the Project**
2. **Create a Feature Branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit Your Changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the Branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Development Guidelines
- Follow PEP 8 Python coding standards
- Add appropriate comments and documentation
- Write test cases
- Ensure code quality

### Issue Reports
If you find bugs or have feature suggestions, please create an Issue:
- Describe the problem in detail
- Provide reproduction steps
- Include relevant log information

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Contributors

- **Chenyuan Liu** - *Project Creator* - [@Chenyuan Liu](https://github.com/chenyuanliu92)

## 🙏 Acknowledgments

- [ArcSoft](https://www.arcsoft.com.cn/) - Providing face recognition SDK
- [Flask](https://flask.palletsprojects.com/) - Web framework
- [OpenCV](https://opencv.org/) - Computer vision library
- [Bootstrap](https://getbootstrap.com/) - UI framework

## 📞 Contact

- Issues: [GitHub Issues](https://github.com/yourusername/i-dorm-guard/issues)

---


<div align="center">

**⭐ If this project helps you, please give us a Star!**

*Made with ❤️ by the I-Dorm-Guard Team*

</div>