<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pendaftaran Pengguna</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            max-width: 600px;
            width: 100%;
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 40px 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 14px;
            opacity: 0.9;
        }

        .form-container {
            padding: 40px 30px;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
            font-size: 14px;
        }

        .form-group label .required {
            color: #e74c3c;
            margin-left: 3px;
        }

        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        .form-control:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .form-control::placeholder {
            color: #aaa;
        }

        textarea.form-control {
            resize: vertical;
            min-height: 100px;
        }

        select.form-control {
            cursor: pointer;
            appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%23333' d='M6 9L1 4h10z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 15px center;
            padding-right: 40px;
        }

        .radio-group,
        .checkbox-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .radio-item,
        .checkbox-item {
            display: flex;
            align-items: center;
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .radio-item:hover,
        .checkbox-item:hover {
            border-color: #667eea;
            background: #f8f9ff;
        }

        .radio-item input[type="radio"],
        .checkbox-item input[type="checkbox"] {
            margin-right: 10px;
            width: 18px;
            height: 18px;
            cursor: pointer;
        }

        .radio-item label,
        .checkbox-item label {
            margin: 0;
            cursor: pointer;
            flex: 1;
            font-weight: normal;
        }

        .file-upload {
            position: relative;
            display: inline-block;
            width: 100%;
        }

        .file-upload-input {
            display: none;
        }

        .file-upload-label {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px;
            border: 2px dashed #ccc;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: #fafafa;
        }

        .file-upload-label:hover {
            border-color: #667eea;
            background: #f8f9ff;
        }

        .file-upload-icon {
            margin-right: 10px;
            font-size: 20px;
        }

        .file-name {
            margin-top: 10px;
            font-size: 12px;
            color: #666;
        }

        .btn-submit {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 10px;
        }

        .btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .btn-submit:active {
            transform: translateY(0);
        }

        .btn-submit:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        .success-message {
            display: none;
            text-align: center;
            padding: 40px;
        }

        .success-message.show {
            display: block;
        }

        .success-icon {
            font-size: 60px;
            color: #4CAF50;
            margin-bottom: 20px;
        }

        .success-message h2 {
            color: #333;
            margin-bottom: 10px;
        }

        .success-message p {
            color: #666;
        }

        .error-message {
            color: #e74c3c;
            font-size: 12px;
            margin-top: 5px;
            display: none;
        }

        @media (max-width: 480px) {
            .header {
                padding: 30px 20px;
            }

            .header h1 {
                font-size: 24px;
            }

            .form-container {
                padding: 30px 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📝 Formulir Pendaftaran</h1>
            <p>Silakan lengkapi data di bawah ini untuk mendaftar</p>
        </div>

        <div class="form-container" id="formContainer">
            <!-- 
                PENTING: 
                1. action mengarah ke API Web3Forms
                2. method harus POST
                3. enctype multipart/form-data diperlukan jika ada upload file
            -->
            <form id="registrationForm" action="https://api.web3forms.com/submit" method="POST" enctype="multipart/form-data">
                
                <!-- Access Key Web3Forms (Hidden) -->
                <input type="hidden" name="access_key" value="5a58df98-c319-4aa1-a9ea-2ae4117eca4d">

                <!-- Subject Email (Opsional, agar mudah dikenali di inbox) -->
                <input type="hidden" name="subject" value="Pendaftaran Pengguna Baru">

                <!-- Nama Lengkap -->
                <div class="form-group">
                    <label for="fullName">Nama Lengkap <span class="required">*</span></label>
                    <input type="text" id="fullName" name="Nama_Lengkap" class="form-control" placeholder="Masukkan nama lengkap Anda" required>
                </div>

                <!-- Email -->
                <div class="form-group">
                    <label for="email">Email <span class="required">*</span></label>
                    <input type="email" id="email" name="Email" class="form-control" placeholder="contoh@email.com" required>
                </div>

                <!-- Nomor Telepon -->
                <div class="form-group">
                    <label for="phone">Nomor Telepon <span class="required">*</span></label>
                    <input type="tel" id="phone" name="Nomor_Telepon" class="form-control" placeholder="08xxxxxxxxxx" required>
                </div>

                <!-- Tanggal Lahir -->
                <div class="form-group">
                    <label for="birthdate">Tanggal Lahir</label>
                    <input type="date" id="birthdate" name="Tanggal_Lahir" class="form-control">
                </div>

                <!-- Jenis Kelamin -->
                <div class="form-group">
                    <label>Jenis Kelamin <span class="required">*</span></label>
                    <div class="radio-group">
                        <div class="radio-item">
                            <input type="radio" id="male" name="Jenis_Kelamin" value="Laki-laki" required>
                            <label for="male">Laki-laki</label>
                        </div>
                        <div class="radio-item">
                            <input type="radio" id="female" name="Jenis_Kelamin" value="Perempuan">
                            <label for="female">Perempuan</label>
                        </div>
                    </div>
                </div>

                <!-- Alamat -->
                <div class="form-group">
                    <label for="address">Alamat Lengkap</label>
                    <textarea id="address" name="Alamat" class="form-control" placeholder="Masukkan alamat lengkap Anda"></textarea>
                </div>

                <!-- Kota -->
                <div class="form-group">
                    <label for="city">Kota</label>
                    <input type="text" id="city" name="Kota" class="form-control" placeholder="Masukkan kota Anda">
                </div>

                <!-- Pekerjaan -->
                <div class="form-group">
                    <label for="occupation">Pekerjaan</label>
                    <select id="occupation" name="Pekerjaan" class="form-control">
                        <option value="">Pilih Pekerjaan</option>
                        <option value="Pelajar/Mahasiswa">Pelajar/Mahasiswa</option>
                        <option value="Karyawan">Karyawan</option>
                        <option value="Wirausaha">Wirausaha</option>
                        <option value="Freelancer">Freelancer</option>
                        <option value="Lainnya">Lainnya</option>
                    </select>
                </div>

                <!-- Upload Foto -->
                <div class="form-group">
                    <label for="photo">Upload Foto Profil (Opsional)</label>
                    <div class="file-upload">
                        <input type="file" id="photo" name="attachment" class="file-upload-input" accept="image/*">
                        <label for="photo" class="file-upload-label">
                            <span class="file-upload-icon">📷</span>
                            <span>Klik untuk upload foto</span>
                        </label>
                        <div class="file-name" id="fileName"></div>
                    </div>
                </div>

                <!-- Hobi -->
                <div class="form-group">
                    <label>Hobi (Pilih yang sesuai)</label>
                    <div class="checkbox-group">
                        <div class="checkbox-item">
                            <input type="checkbox" id="reading" name="Hobi" value="Membaca">
                            <label for="reading">Membaca</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="sports" name="Hobi" value="Olahraga">
                            <label for="sports">Olahraga</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="traveling" name="Hobi" value="Traveling">
                            <label for="traveling">Traveling</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="cooking" name="Hobi" value="Memasak">
                            <label for="cooking">Memasak</label>
                        </div>
                    </div>
                </div>

                <!-- Pesan Tambahan -->
                <div class="form-group">
                    <label for="message">Pesan Tambahan</label>
                    <textarea id="message" name="Pesan_Tambahan" class="form-control" placeholder="Tulis pesan atau informasi tambahan..."></textarea>
                </div>

                <!-- Tombol Submit -->
                <button type="submit" class="btn-submit" id="submitBtn">Daftar Sekarang</button>
                <div class="error-message" id="errorMessage"></div>
            </form>
        </div>

        <!-- Pesan Sukses -->
        <div class="success-message" id="successMessage">
            <div class="success-icon">✅</div>
            <h2>Pendaftaran Berhasil!</h2>
            <p>Data Anda telah dikirim. Silakan cek email konfirmasi.</p>
            <button onclick="location.reload()" class="btn-submit" style="margin-top: 20px;">Kembali</button>
        </div>
    </div>

    <script>
        // File upload handler
        const photoInput = document.getElementById('photo');
        const fileName = document.getElementById('fileName');

        photoInput.addEventListener('change', function(e) {
            if (e.target.files.length > 0) {
                fileName.textContent = 'File terpilih: ' + e.target.files[0].name;
            } else {
                fileName.textContent = '';
            }
        });

        // Form submission handler using Fetch API
        const form = document.getElementById('registrationForm');
        const formContainer = document.getElementById('formContainer');
        const successMessage = document.getElementById('successMessage');
        const submitBtn = document.getElementById('submitBtn');
        const errorMessage = document.getElementById('errorMessage');

        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Disable button to prevent double submit
            submitBtn.disabled = true;
            submitBtn.textContent = 'Mengirim...';
            errorMessage.style.display = 'none';

            // Collect form data
            const formData = new FormData(form);

            // Send data to Web3Forms
            fetch('https://api.web3forms.com/submit', {
                method: 'POST',
                body: formData
            })
            .then(response => response.json())
            .then(data => {
                if (data.success) {
                    // Show success message
                    formContainer.style.display = 'none';
                    successMessage.classList.add('show');
                    
                    // Reset form
                    form.reset();
                    fileName.textContent = '';
                } else {
                    // Show error message
                    errorMessage.textContent = 'Terjadi kesalahan: ' + (data.message || 'Silakan coba lagi.');
                    errorMessage.style.display = 'block';
                    submitBtn.disabled = false;
                    submitBtn.textContent = 'Daftar Sekarang';
                }
            })
            .catch(error => {
                console.error('Error:', error);
                errorMessage.textContent = 'Gagal terhubung ke server. Silakan periksa koneksi internet Anda.';
                errorMessage.style.display = 'block';
                submitBtn.disabled = false;
                submitBtn.textContent = 'Daftar Sekarang';
            });
        });

        // Phone number formatting
        const phoneInput = document.getElementById('phone');
        phoneInput.addEventListener('input', function(e) {
            let value = e.target.value.replace(/\D/g, '');
            if (value.length > 0 && value[0] === '0') {
                value = value.substring(1);
            }
            if (value.length > 12) {
                value = value.substring(0, 12);
            }
            e.target.value = value;
        });
    </script>
</body>
</html>
