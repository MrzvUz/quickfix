# Required environment set up:
To install Python QuickFix Library or develop custom QuickFix Library we need to set up an environment and install required all dependencies. I will be using Linux CentOS 7 for this demo.

    a. Install Python.
    
        1. Update your OS or you can update and upgrade at the same time:

            sudo yum -y update && sudo yum -y upgrade
        
        2. Install below pre-requisites for Python and Python Quickfix library:

            sudo yum groupinstall "Development Tools" -y
            sudo yum install -y gcc open-ssl-devel bzip2-devel libffi-devel wget make gcc gcc-c++ glibc-devel 

        3. Download Python 3.9.7 setup in /tmp location and unzip tgz file:

            cd /tmp/
            wget https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tgz            
            tar xzf Python-3.9.7.tgz

        4. Install Python 3.9.7 with alternate installation.

            cd Python-3.9.7
            ./configure --enable-optimizations            
            sudo make altinstall

        5. Set currently installed Python 3.9.7 as a default Linux Python version:

            sudo ln -sfn /usr/local/bin/python3.9 /usr/bin/python3.9
            sudo ln -sfn /usr/local/bin/pip3.9 /usr/bin/pip3.9

        6. Verify new Python 3.9.7 and PIP version:

            python3.9 -V
            pip3.9 -V

# Packaging custom Python QuickFix Library.
Make sure that before packaging any Python libraries your PIP and SETUPTOOLS are updated.
    
    b. Install, update and upgrade necessary dependencies.

        1. Update and upgrade pip, setuptools and wheel:

            python3.9 -m pip install --upgrade pip setuptools wheel

        2. Download quickfix repository:

            wget https://files.pythonhosted.org/packages/62/b0/caf2dfae8779551f6e1d2bc78668d8f5a2303d21311fdd54345722b68cbc/quickfix-1.15.1.tar.gz
            tar -xvf quickfix-1.15.1.tar.gz
            cd quickfix-1.15.1

        3. Create MANIFEST.in file to include all folders and files in quickfix-1.15.1 folder. To do that put the script below.

            include *.cpp
            include *.xml
            include C++/*.cc
            include C++/*.h
            include C++/*.cpp
            include C++/*.hpp
            include C++/double-conversion/*.cc
            include C++/double-conversion/*.c
            include C++/double-conversion/*.h

        4. Create LICENSE file and modify your Licensing information.

            MIT License

            Copyright (c) 2021 Your Name

            Permission is hereby granted, free of charge, to any person obtaining a copy
            of this software and associated documentation files (the "Software"), to deal
            in the Software without restriction, including without limitation the rights
            to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
            copies of the Software, and to permit persons to whom the Software is
            furnished to do so, subject to the following conditions:

            The above copyright notice and this permission notice shall be included in all
            copies or substantial portions of the Software.

            THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
            IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
            FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
            AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
            LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
            OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
            SOFTWARE.

        5. Create pyproject.toml file and put the script below:

            [build-system]
            requires = [
                "setuptools>=54",
                "wheel"
            ]
            build-backend = "setuptools.build_meta"

        6. Create setup.cfg file and put the script below:

            [metadata]
            name = quickfix
            version = 0.0.1
            author = Your Name
            author_email = example@gmail.com
            description = Market routing inbound fix messages.
            long_description = file: README.md
            long_description_content_type = text/markdown
            url = https://github.com/mrzvuz/quickfix
            classifiers =
                Programming Language :: Python :: 3
                License :: OSI Approved :: MIT License
                Operating System :: OS Independent

            [options]
            packages = find:
            python_requires = >=3.6
            include_package_data = True

        7. Create __init__.py file which will pick up all .py files and will include in the package.

            touch __init__.py

# Packaging Python QuickFix Library.
Once you have gone through all the steps above, now it is time to packaging our custom Python QuickFix Library.

    c. Change your directory into quickfix-1.15.1 and run following commands:

        1. To build our python library we should install build module:

            pip3.9 install build
        
        2. Finally from root directory of quickfix-1.15.1 run:

            python3.9 -m build
            











