import React, { useState, useEffect } from 'react';
import { 
  BookOpen, Award, MessageSquare, UserCheck, LogOut, Key, Mail, User, 
  Search, CheckCircle2, XCircle, Clock, ChevronRight, GraduationCap, 
  Sparkles, FileText, Send, Lock, HelpCircle, ArrowLeft, RefreshCw, BarChart2,
  Calendar, Check, ShieldCheck, HeartHandshake, Home, PlayCircle, Volume2, 
  Download, Printer, Filter, CheckCircle, AlertCircle, Edit3, Save, ChevronLeft,
  Users, MessageCircle, Info, Star, Bookmark, Tag, Briefcase, ChevronDown, X, Building
} from 'lucide-react';

// ==========================================
// DATA KURIKULUM, MATERI & FORMATIF
// ==========================================

const LEVELS = [
  { id: 'SD', name: 'Sekolah Dasar (SD)', grades: ['Kelas 1', 'Kelas 2', 'Kelas 3', 'Kelas 4', 'Kelas 5', 'Kelas 6'] },
  { id: 'SMP', name: 'Sekolah Menengah Pertama (SMP)', grades: ['Kelas 7', 'Kelas 8', 'Kelas 9'] },
  { id: 'SMA', name: 'Sekolah Menengah Atas (SMA)', grades: ['Kelas 10', 'Kelas 11', 'Kelas 12'] },
];

const SUBJECTS_LIST = [
  { id: 'matematika', name: 'Matematika', icon: '📐', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'ipa', name: 'IPA (Ilmu Pengetahuan Alam)', icon: '🔬', cat: ['SD', 'SMP'] },
  { id: 'ips', name: 'IPS (Ilmu Pengetahuan Sosial)', icon: '🌍', cat: ['SD', 'SMP'] },
  { id: 'pkn', name: 'Pendidikan Pancasila & Kewarganegaraan', icon: '🇮🇩', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'bindonesia', name: 'Bahasa Indonesia', icon: '📚', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'binggris', name: 'Bahasa Inggris', icon: '🔤', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'barab', name: 'Bahasa Arab', icon: '🕌', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'tahfidz', name: 'Tahfidz Al-Qur\'an', icon: '📖', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'tahsin', name: 'Tahsin Al-Qur\'an', icon: '✨', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'fisika', name: 'Fisika', icon: '⚡', cat: ['SMA'] },
  { id: 'kimia', name: 'Kimia', icon: '🧪', cat: ['SMA'] },
  { id: 'biologi', name: 'Biologi', icon: '🧬', cat: ['SMA'] },
  { id: 'geografi', name: 'Geografi', icon: '🗺️', cat: ['SMA'] },
  { id: 'sosiologi', name: 'Sosiologi', icon: '👥', cat: ['SMA'] },
  { id: 'ekonomi', name: 'Ekonomi', icon: '📊', cat: ['SMA'] },
  { id: 'sejarah', name: 'Sejarah', icon: '🏛️', cat: ['SMA'] },
  { id: 'pjok', name: 'PJOK (Pendidikan Jasmani & Kesehatan)', icon: '⚽', cat: ['SD', 'SMP', 'SMA'] },
  { id: 'pai', name: 'Pendidikan Agama Islam (PAI)', icon: '☪️', cat: ['SD', 'SMP', 'SMA'] },
];

// Data Artikel Edukasi
const ARTICLES_DATA = [
  {
    id: 1,
    title: 'Strategi Efektif Menguasai Soal HOTS Matematika & Fisika',
    category: 'Metode Belajar',
    date: '28 Oktober',
    readTime: '5 min baca',
    summary: 'Tips dan logika berpikir cepat dalam menyelesaikan soal Higher Order Thinking Skills tanpa menghafal rumus rumit.',
    content: 'Menguasai soal HOTS memerlukan pemahaman konsep dasar yang kuat dan kemampuan menghubungkan berbagai teorema. Pertama, identifikasi variabel utama dalam soal. Kedua, gunakan metode diagram visual untuk merumuskan masalah...'
  },
  {
    id: 2,
    title: 'Panduan Mudah Menghafal Al-Qur\'an (Tahfidz & Tahsin) untuk Pelajar',
    category: 'Keislaman',
    date: '25 Oktober',
    readTime: '4 min baca',
    summary: 'Metode Murajaah harian dan perbaikan tajwid agar hafalan kuat dan tidak mudah lupa di tengah kesibukan sekolah.',
    content: 'Kunci utama dalam program Tahfidz di Scientists Learning Center adalah mengombinasikan metode Tikrar (pengulangan 20x) dengan perbaikan makhraj huruf (Tahsin) secara berkala sebelum menambah ayat baru...'
  },
  {
    id: 3,
    title: 'Persiapan Menghadapi Asesmen Formatif & Ujian Nasional',
    category: 'Ujian & Asesmen',
    date: '20 Oktober',
    readTime: '6 min baca',
    summary: 'Manfaatkan 10 siklus Formatif terstruktur untuk mengukur kesiapan belajar dan mencapai nilai raport maksimal.',
    content: 'Evaluasi formatif yang dilakukan secara berkala terbukti meningkatkan retensi memori hingga 80%. Latihan 20 soal simulasi per materi membantu mengidentifikasi kelemahan bab dengan lebih akurat...'
  }
];

// Data Keunggulan
const ADVANTAGES_DATA = [
  { icon: '📚', title: '18 Mata Pelajaran Lengkap', desc: 'Menjangkau Matematika, Sains, Sosial, Bahasa, hingga Tahfidz & Tahsin Al-Qur\'an.' },
  { icon: '🎯', title: '10 Siklus Formatif (20 Soal/Mapel)', desc: 'Setiap mata pelajaran dilengkapi 10 urutan Formatif interaktif dengan timer dan pembahasannya.' },
  { icon: '🕌', title: 'Program Tahfidz & Tahsin', desc: 'Pendampingan khusus tajwid dan hafalan Al-Qur\'an terintegrasi dengan pembelajaran sekolah.' },
  { icon: '👨‍🏫', title: 'Live Consultation & Forum Tutor', desc: 'Diskusi PR dan tanya jawab interaktif bersama tutor berpengalaman setiap hari.' },
  { icon: '📊', title: 'Raport Digital & Cetak Transkrip', desc: 'Pantau grafik ketercapaian belajar siswa dan cetak raport formatif secara langsung.' },
  { icon: '⚡', title: 'Akses 24/7 Kurikulum Nasional', desc: 'Rangkuman materi komprehensif Semester 1 dan 2 dapat diakses kapan saja.' }
];

// Data Testimoni
const TESTIMONIALS_DATA = [
  { name: 'Nabila Syakieb', role: 'Siswa SMA Kelas 11', text: 'Sangat terbantu dengan 10 urutan Formatifnya! Soal 20 nomornya lengkap dengan pembahasan yang bikin paham konsep Fisika dan Kimia.', rating: 5 },
  { name: 'Drs. Hendra Wijaya', role: 'Orang Tua Siswa SD', text: 'Anak saya makin bersemangat belajar. Fitur Tahfidz & Tahsin sangat berguna disamping pelajaran umum Matematika & IPA.', rating: 5 },
  { name: 'Fathir Ahmad', role: 'Siswa SMP Kelas 8', text: 'Fitur Live Consultation Tutor mantap sekali, kalau ada PR susah tinggal tanyakan langsung di forum dan dijawab cepat.', rating: 5 }
];

// Data FAQ
const FAQS_DATA = [
  { q: 'Apakah Scientists Learning Center mencakup semua jenjang sekolah?', a: 'Ya! Kami menyediakan bimbingan belajar lengkap dari SD (Kelas 1-6), SMP (Kelas 7-9), hingga SMA (Kelas 10-12) sesuai standar Kurikulum Nasional.' },
  { q: 'Bagaimana sistem Evaluasi Formatif 1-10 bekerja?', a: 'Setiap mata pelajaran memiliki 10 urutan soal formatif. Masing-masing formatif berisi 20 soal interaktif, waktu 20 menit, skor otomatis, dan penjelasan kunci jawaban detail.' },
  { q: 'Apakah ada materi Agama dan Al-Qur\'an?', a: 'Tentu. Selain pelajaran umum, kami menyediakan materi Pendidikan Agama Islam (PAI), Bahasa Arab, Tahfidz Al-Qur\'an, dan Tahsin Al-Qur\'an.' },
  { q: 'Bagaimana cara mendaftar akun di aplikasi?', a: 'Anda dapat mendaftar dengan menekan tombol "Daftar Akun" di bagian atas halaman, atau masuk dengan 1-klik menggunakan Akun Google.' }
];

// Data Promo
const PROMOS_DATA = [
  { code: 'SLCJUARA50', discount: 'Diskon 50%', desc: 'Promo Pendaftaran Paket Semester Ganjil & Genap All-In-One', valid: 'Berlaku s/d Akhir Bulan' },
  { code: 'SLCSAHABAT', discount: 'Gratis 1 Bulan', desc: 'Voucher Tambahan Akses Modul Tahfidz & Live Zoom Bimbel', valid: 'Terbatas 100 Kuota Pertama' }
];

// Data Lowongan Kerja
const VACANCIES_DATA = [
  { title: 'Tutor Pengajar Matematika & IPA (SD/SMP)', type: 'Full-Time / Part-Time', loc: 'Online / Hybrid', req: 'S1 Pendidikan / Sains, komunikatif & sabar mengajar anak-anak.' },
  { title: 'Tutor Fisika, Kimia & Biologi (SMA)', type: 'Part-Time', loc: 'Online', req: 'S1 MIPA / Teknik, berpengalaman mengajar soal HOTS & Olimpiade.' },
  { title: 'Pengajar Tahfidz & Tahsin Al-Qur\'an', type: 'Part-Time', loc: 'Online', req: 'Memiliki hafalan Al-Qur\'an min. 5 Juz & sanad/ijazah Tahsin mutqin.' }
];

// Generator Rangkuman Materi Lengkap Semester 1 & 2
const generateDetailedMaterials = (subjectName, grade) => ({
  sem1: [
    {
      bab: 1,
      title: `Bab 1: Konsep Fundamental & Prinsip Dasar ${subjectName}`,
      summary: `Pembahasan menyeluruh mengenai pondasi utama materi ${subjectName} untuk ${grade} pada Semester 1. Fokus pada definisi kunci, teorema utama, dan penerapannya dalam Kurikulum Nasional.`,
      points: [
        `Pengenalan istilah dasar dan variabel penting dalam ${subjectName}.`,
        `Hukum & Asas Utama yang berlaku secara konseptual.`,
        `Metode analisis terstruktur untuk pemecahan masalah sederhana.`
      ]
    },
    {
      bab: 2,
      title: `Bab 2: Analisis & Pemecahan Masalah Terpadu`,
      summary: `Studi kasus dan teknik kalkulasi lanjutan untuk memperdalam pemahaman materi semester ganjil. Melatih berpikir kritis dan analitis.`,
      points: [
        `Identifikasi rumusan masalah dan pola umum.`,
        `Formulasi rumus cepat (Quick Formula) & trik penyelesaian.`,
        `Latihan studi kasus kontekstual kehidupan sehari-hari.`
      ]
    },
    {
      bab: 3,
      title: `Bab 3: Aplikasional & Eksperimen Lapangan`,
      summary: `Rangkuman fakta penting, peragaan praktis, dan ulasan persiapan Penilaian Tengah Semester (PTS).`,
      points: [
        `Penerapan praktis pada pengamatan lapangan / laboratorium.`,
        `Rangkuman formula inti & tabel perbandingan variabel.`,
        `Simulasi soal-soal latihan standar Kurikulum Nasional.`
      ]
    }
  ],
  sem2: [
    {
      bab: 4,
      title: `Bab 4: Pengembangan Teori & Pendalaman Materi`,
      summary: `Memasuki Semester 2, siswa diajak mempelajari materi tingkat lanjut dengan komprehensif, mencakup integrasi antar topik.`,
      points: [
        `Korelasi materi Bab 4 dengan bab-bab di semester sebelumnya.`,
        `Pengembangan formula tingkat tinggi & pemodelan numerik/teoretis.`,
        `Latihan menganalisis grafik, struktur, atau diagram.`
      ]
    },
    {
      bab: 5,
      title: `Bab 5: Studi Komparatif & Penalaran Tingkat Tinggi (HOTS)`,
      summary: `Pengayaan materi berbasis High Order Thinking Skills (HOTS) untuk mempersiapkan siswa menghadapi penilaian akhir tahun.`,
      points: [
        `Analisis mendalam mengenai fenomena khusus dalam ${subjectName}.`,
        `Teknik eliminasi cepat pada soal-soal pilihan ganda kompleks.`,
        `Pembahasan contoh soal ujian nasional & olimpiade dasar.`
      ]
    },
    {
      bab: 6,
      title: `Bab 6: Rangkuman Komprehensif & Kilas Balik`,
      summary: `Sintesis dari seluruh bab di Semester 1 dan 2 sebagai persiapan akhir menghadapi Ujian Kenaikan Kelas (UKK).`,
      points: [
        `Peta Konsep (Mind Map) keseluruhan materi ${subjectName}.`,
        `Kumpulan rumus ringkas & Glosarium istilah penting.`,
        `Checklist kesiapan siswa sebelum mengikuti Ujian Akhir.`
      ]
    }
  ]
});

// Generator 20 Soal per Formatif (1 - 10)
const generate20FormativeQuestions = (subjectName, formativeNum) => {
  const optionsLetters = ['A', 'B', 'C', 'D'];
  return Array.from({ length: 20 }, (_, index) => {
    const qNum = index + 1;
    const correctIdx = (qNum + formativeNum * 3) % 4;
    return {
      id: qNum,
      question: `[Soal No. ${qNum} - Formatif ${formativeNum}] Berdasarkan indikator Kurikulum Nasional untuk ${subjectName}, manakah analisis yang paling akurat berikut ini?`,
      options: [
        `Opsi A: Hasil formulasi pada sub-materi ${formativeNum}.${qNum} menunjukkan efisiensi konseptual optimal.`,
        `Opsi B: Nilai konstanta dan variabel ${subjectName} berbanding lurus dengan parameter utama.`,
        `Opsi C: Implementasi prinsip dasar bab ${formativeNum} menghasilkan verifikasi logis yang valid.`,
        `Opsi D: Karakteristik fenomena ${subjectName} pada indikator ${qNum} memenuhi kaidah standar.`
      ],
      correctAnswer: correctIdx,
      explanation: `Pembahasan Soal No. ${qNum}: Berdasarkan acuan Kurikulum Nasional materi ${subjectName} (Formatif ${formativeNum}), pilihan jawaban '${optionsLetters[correctIdx]}' adalah yang paling rasional karena sesuai dengan teori utama di Bab ${Math.ceil(qNum / 4)}.`
    };
  });
};

export default function App() {
  // ------------------------------------------
  // STATE MANAGEMENT
  // ------------------------------------------

  // Auth States
  const [currentUser, setCurrentUser] = useState(null);
  const [authModalOpen, setAuthModalOpen] = useState(false);
  const [authView, setAuthView] = useState('login'); // 'login', 'register', 'forgot'
  const [authForm, setAuthForm] = useState({
    username: '',
    fullName: '',
    email: '',
    password: '',
    level: 'SMA',
    grade: 'Kelas 10'
  });
  const [authNotification, setAuthNotification] = useState(null);

  // Landing Page Interactive States
  const [landingTab, setLandingTab] = useState('beranda'); // 'beranda', 'artikel', 'keunggulan', 'testimoni', 'faq', 'promo', 'lowongan'
  const [selectedArticle, setSelectedArticle] = useState(null);
  const [openFaqIndex, setOpenFaqIndex] = useState(0);
  const [copiedCode, setCopiedCode] = useState('');
  const [selectedJob, setSelectedJob] = useState(null);
  const [jobAppliedSuccess, setJobAppliedSuccess] = useState(false);

  // Dashboard Nav States (When Logged In)
  const [activeTab, setActiveTab] = useState('pembelajaran'); // 'pembelajaran', 'evaluasi', 'interaksi', 'manajemen'
  const [selectedLevel, setSelectedLevel] = useState('SMA');
  const [selectedGrade, setSelectedGrade] = useState('Kelas 10');
  const [selectedSubject, setSelectedSubject] = useState(SUBJECTS_LIST[0]);
  const [searchTerm, setSearchTerm] = useState('');

  // Active Formative Quiz State
  const [selectedFormativeNum, setSelectedFormativeNum] = useState(null); // 1-10
  const [quizAnswers, setQuizAnswers] = useState({});
  const [currentQuestionIndex, setCurrentQuestionIndex] = useState(0);
  const [quizSubmitted, setQuizSubmitted] = useState(false);
  const [quizTimer, setQuizTimer] = useState(1200); // 20 mins

  // Interaction State (Forum, Chat, Schedule)
  const [activeSubInteraksi, setActiveSubInteraksi] = useState('forum');
  const [discussions, setDiscussions] = useState([
    { id: 1, user: 'Ahmad Raihan', grade: 'SMA Kelas 10', subject: 'Fisika', title: 'Bagaimana membedakan GLB dan GLBB secara praktis?', replies: 4, time: '15 menit lalu' },
    { id: 2, user: 'Nabila Syakieb', grade: 'SMP Kelas 8', subject: 'Matematika', title: 'Tips cepat hafal rumus Luas Permukaan Prisma?', replies: 6, time: '1 jam lalu' },
    { id: 3, user: 'Fathir Ahmad', grade: 'SD Kelas 5', subject: 'IPA', title: 'Mengapa siklus air tidak pernah habis di bumi?', replies: 2, time: '3 jam lalu' }
  ]);
  const [newPost, setNewPost] = useState({ subject: 'Matematika', title: '' });
  const [chatMessages, setChatMessages] = useState([
    { id: 1, sender: 'Tutor SLC', role: 'tutor', text: 'Selamat datang di Consultation Room Scientists Learning Center! Silakan ajukan pertanyaanmu mengenai materi pelajaran.', time: '09:00' }
  ]);
  const [chatInput, setChatInput] = useState('');

  // Management State
  const [isEditingProfile, setIsEditingProfile] = useState(false);
  const [userProfileData, setUserProfileData] = useState({
    bio: 'Siswa aktif Scientists Learning Center yang bersemangat menguasai Kurikulum Nasional.',
    phone: '0812-3456-7890',
    schoolOrigin: 'SMA Negeri 1 Jakarta'
  });

  // Keep active subject compatible with level
  useEffect(() => {
    const validSubjects = SUBJECTS_LIST.filter(s => s.cat.includes(selectedLevel));
    if (validSubjects.length > 0 && !validSubjects.some(s => s.id === selectedSubject.id)) {
      setSelectedSubject(validSubjects[0]);
    }
  }, [selectedLevel]);

  // Quiz Timer Effect
  useEffect(() => {
    let timerInterval = null;
    if (selectedFormativeNum && !quizSubmitted && quizTimer > 0) {
      timerInterval = setInterval(() => {
        setQuizTimer(prev => prev - 1);
      }, 1000);
    } else if (quizTimer === 0 && selectedFormativeNum && !quizSubmitted) {
      setQuizSubmitted(true);
    }
    return () => clearInterval(timerInterval);
  }, [selectedFormativeNum, quizSubmitted, quizTimer]);

  // ------------------------------------------
  // AUTH HANDLERS
  // ------------------------------------------
  const openAuth = (view) => {
    setAuthView(view);
    setAuthNotification(null);
    setAuthModalOpen(true);
  };

  const handleLoginSubmit = (e) => {
    e.preventDefault();
    if (!authForm.username || !authForm.password) {
      setAuthNotification({ type: 'error', text: 'Mohon isi Username / Email dan Password!' });
      return;
    }
    setCurrentUser({
      username: authForm.username,
      fullName: authForm.fullName || authForm.username,
      email: authForm.email || `${authForm.username}@gmail.com`,
      level: selectedLevel,
      grade: selectedGrade,
      avatar: '👨‍🎓'
    });
    setAuthModalOpen(false);
  };

  const handleGoogleLoginMock = () => {
    setCurrentUser({
      username: 'google_student',
      fullName: 'Siswa Akun Google',
      email: 'siswa.google@gmail.com',
      level: selectedLevel,
      grade: selectedGrade,
      avatar: '🌐'
    });
    setAuthModalOpen(false);
  };

  const handleRegisterSubmit = (e) => {
    e.preventDefault();
    if (!authForm.username || !authForm.fullName || !authForm.email || !authForm.password) {
      setAuthNotification({ type: 'error', text: 'Semua bidang registrasi wajib diisi!' });
      return;
    }
    setCurrentUser({
      username: authForm.username,
      fullName: authForm.fullName,
      email: authForm.email,
      level: authForm.level,
      grade: authForm.grade,
      avatar: '🌟'
    });
    setSelectedLevel(authForm.level);
    setSelectedGrade(authForm.grade);
    setAuthModalOpen(false);
  };

  const handleForgotSubmit = (e) => {
    e.preventDefault();
    if (!authForm.email) {
      setAuthNotification({ type: 'error', text: 'Masukkan Email Anda yang terdaftar!' });
      return;
    }
    setAuthNotification({ type: 'success', text: 'Tautan reset password telah dikirimkan ke email Anda!' });
  };

  const handleLogout = () => {
    setCurrentUser(null);
    setLandingTab('beranda');
    setSelectedFormativeNum(null);
  };

  // Quiz Handlers
  const startQuiz = (formativeNum) => {
    setSelectedFormativeNum(formativeNum);
    setQuizAnswers({});
    setCurrentQuestionIndex(0);
    setQuizSubmitted(false);
    setQuizTimer(1200); // 20 mins
  };

  const calculateScore = (questions) => {
    let correctCount = 0;
    questions.forEach(q => {
      if (quizAnswers[q.id] === q.correctAnswer) {
        correctCount += 1;
      }
    });
    return Math.round((correctCount / questions.length) * 100);
  };

  const sendChatMessage = (e) => {
    e.preventDefault();
    if (!chatInput.trim()) return;
    const newMsg = {
      id: Date.now(),
      sender: currentUser.fullName,
      role: 'student',
      text: chatInput,
      time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    };
    setChatMessages(prev => [...prev, newMsg]);
    setChatInput('');
    setTimeout(() => {
      setChatMessages(prev => [
        ...prev,
        {
          id: Date.now() + 1,
          sender: 'Tutor SLC',
          role: 'tutor',
          text: 'Pertanyaan yang bagus! Tutor kami sedang meninjau materi terkait untuk memberikan jawaban paling komprehensif.',
          time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
        }
      ]);
    }, 1200);
  };

  const filteredSubjectsList = SUBJECTS_LIST.filter(sub => 
    sub.cat.includes(selectedLevel) &&
    sub.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  // ==========================================
  // VIEW 1: PUBLIC LANDING PAGE (UNAUTHENTICATED VIEW)
  // ==========================================
  if (!currentUser) {
    return (
      <div className="min-h-screen bg-slate-900 text-slate-100 flex flex-col font-sans selection:bg-teal-500 selection:text-white">
        
        {/* PUBLIC TOP NAVIGATION BAR */}
        <header className="bg-gradient-to-r from-blue-950 via-slate-900 to-teal-950 border-b border-white/10 sticky top-0 z-40 backdrop-blur-md">
          <div className="max-w-7xl mx-auto px-4 sm:px-6 py-3 flex flex-wrap items-center justify-between gap-4">
            
            {/* Logo Brand */}
            <div 
              onClick={() => setLandingTab('beranda')}
              className="flex items-center gap-3 cursor-pointer group"
            >
              <div className="w-10 h-10 rounded-2xl bg-gradient-to-tr from-blue-600 via-teal-500 to-emerald-400 text-white flex items-center justify-center shadow-lg group-hover:scale-105 transition border border-white/20">
                <GraduationCap className="w-6 h-6" />
              </div>
              <div>
                <h1 className="font-black text-base sm:text-lg tracking-tight leading-none text-white group-hover:text-teal-300 transition">
                  Scientists Learning Center
                </h1>
                <p className="text-[10px] text-emerald-400 font-bold uppercase tracking-wider mt-0.5">
                  Bimbel Kurikulum Nasional SD • SMP • SMA
                </p>
              </div>
            </div>

            {/* Navigation Links */}
            <nav className="hidden md:flex items-center gap-1 bg-white/5 p-1 rounded-2xl border border-white/10">
              {[
                { id: 'beranda', label: 'Beranda', icon: Home },
                { id: 'artikel', label: 'Artikel', icon: FileText },
                { id: 'keunggulan', label: 'Keunggulan', icon: Sparkles },
                { id: 'testimoni', label: 'Testimoni', icon: Star },
                { id: 'faq', label: 'FAQ', icon: HelpCircle },
                { id: 'promo', label: 'Promo', icon: Tag },
                { id: 'lowongan', label: 'Lowongan', icon: Briefcase },
              ].map((item) => {
                const Icon = item.icon;
                const isActive = landingTab === item.id;
                return (
                  <button
                    key={item.id}
                    onClick={() => setLandingTab(item.id)}
                    className={`px-3 py-1.5 rounded-xl text-xs font-bold transition flex items-center gap-1.5 ${
                      isActive 
                        ? 'bg-gradient-to-r from-teal-500 to-emerald-500 text-white shadow-md' 
                        : 'text-slate-300 hover:text-white hover:bg-white/10'
                    }`}
                  >
                    <Icon className="w-3.5 h-3.5" /> {item.label}
                  </button>
                );
              })}
            </nav>

            {/* Auth Buttons */}
            <div className="flex items-center gap-2">
              <button
                onClick={() => openAuth('login')}
                className="px-4 py-2 rounded-xl bg-white/10 hover:bg-white/20 border border-white/20 text-white text-xs font-extrabold transition shadow-sm"
              >
                Masuk / Login
              </button>
              <button
                onClick={() => openAuth('register')}
                className="px-4 py-2 rounded-xl bg-gradient-to-r from-emerald-500 to-teal-600 hover:from-emerald-600 hover:to-teal-700 text-white text-xs font-extrabold shadow-md transition"
              >
                Daftar Akun
              </button>
            </div>

          </div>

          {/* Mobile Nav Menu Pills */}
          <div className="flex md:hidden items-center gap-1 px-4 py-2 overflow-x-auto border-t border-white/5 bg-slate-950/80">
            {[
              { id: 'beranda', label: 'Beranda' },
              { id: 'artikel', label: 'Artikel' },
              { id: 'keunggulan', label: 'Keunggulan' },
              { id: 'testimoni', label: 'Testimoni' },
              { id: 'faq', label: 'FAQ' },
              { id: 'promo', label: 'Promo' },
              { id: 'lowongan', label: 'Lowongan' },
            ].map(item => (
              <button
                key={item.id}
                onClick={() => setLandingTab(item.id)}
                className={`px-3 py-1 rounded-full text-[11px] font-bold whitespace-nowrap ${
                  landingTab === item.id ? 'bg-teal-500 text-white' : 'text-slate-400 bg-white/5'
                }`}
              >
                {item.label}
              </button>
            ))}
          </div>
        </header>

        {/* PUBLIC BODY SECTIONS */}
        <main className="flex-grow">
          
          {/* ==================== 1. BERANDA ==================== */}
          {landingTab === 'beranda' && (
            <div className="space-y-16 pb-16">
              
              {/* HERO BANNER */}
              <section className="relative overflow-hidden pt-12 pb-20 px-4 sm:px-6 bg-gradient-to-b from-blue-950 via-slate-900 to-slate-900">
                <div className="absolute top-1/4 left-1/2 -translate-x-1/2 w-96 h-96 bg-teal-500/20 rounded-full blur-3xl pointer-events-none"></div>

                <div className="max-w-5xl mx-auto text-center space-y-6 relative z-10">
                  <span className="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-teal-500/10 border border-teal-500/30 text-teal-300 text-xs font-extrabold uppercase tracking-widest backdrop-blur-md">
                    <Sparkles className="w-4 h-4 text-emerald-400" /> Platform Bimbel Kurikulum Nasional Terlengkap
                  </span>

                  <h1 className="text-3xl sm:text-5xl font-black text-white tracking-tight leading-tight">
                    Raih Prestasi Akademik Tertinggi bersama <br />
                    <span className="text-transparent bg-clip-text bg-gradient-to-r from-teal-400 via-emerald-300 to-blue-400">
                      Scientists Learning Center
                    </span>
                  </h1>

                  <p className="text-xs sm:text-base text-slate-300 max-w-3xl mx-auto leading-relaxed">
                    Bimbingan belajar interaktif untuk tingkat SD (1-6), SMP (7-9), dan SMA (10-12). Dilengkapi 18 Mata Pelajaran, Rangkuman Semester 1 & 2, serta Evaluasi 10 Formatif (20 soal interaktif per materi) dan Program Tahfidz/Tahsin Al-Qur'an.
                  </p>

                  <div className="flex flex-wrap items-center justify-center gap-4 pt-4">
                    <button
                      onClick={() => openAuth('register')}
                      className="px-8 py-3.5 rounded-2xl bg-gradient-to-r from-emerald-500 via-teal-600 to-blue-700 hover:from-emerald-600 hover:to-blue-800 text-white font-black text-xs sm:text-sm shadow-xl hover:shadow-teal-500/20 transition transform hover:-translate-y-0.5"
                    >
                      Mulai Belajar Sekarang
                    </button>
                    <button
                      onClick={() => openAuth('login')}
                      className="px-8 py-3.5 rounded-2xl bg-slate-800 hover:bg-slate-700 text-white font-extrabold text-xs sm:text-sm border border-slate-700 transition"
                    >
                      Masuk dengan Akun Google
                    </button>
                  </div>

                  {/* QUICK STATS */}
                  <div className="grid grid-cols-2 md:grid-cols-4 gap-4 pt-10 max-w-4xl mx-auto">
                    <div className="bg-white/5 border border-white/10 p-4 rounded-3xl backdrop-blur-md">
                      <span className="block text-2xl font-black text-teal-400">18 Mapel</span>
                      <span className="text-[11px] text-slate-400 font-semibold uppercase">SD • SMP • SMA</span>
                    </div>
                    <div className="bg-white/5 border border-white/10 p-4 rounded-3xl backdrop-blur-md">
                      <span className="block text-2xl font-black text-emerald-400">10 Formatif</span>
                      <span className="text-[11px] text-slate-400 font-semibold uppercase">Per Mata Pelajaran</span>
                    </div>
                    <div className="bg-white/5 border border-white/10 p-4 rounded-3xl backdrop-blur-md">
                      <span className="block text-2xl font-black text-blue-400">20 Soal</span>
                      <span className="text-[11px] text-slate-400 font-semibold uppercase">Per Siklus Formatif</span>
                    </div>
                    <div className="bg-white/5 border border-white/10 p-4 rounded-3xl backdrop-blur-md">
                      <span className="block text-2xl font-black text-amber-400">Tahfidz & Tahsin</span>
                      <span className="text-[11px] text-slate-400 font-semibold uppercase">Program Khusus</span>
                    </div>
                  </div>

                </div>
              </section>

              {/* JENJANG BELAJAR PREVIEW */}
              <section className="max-w-7xl mx-auto px-4 sm:px-6">
                <div className="text-center space-y-2 mb-8">
                  <h2 className="text-2xl font-extrabold text-white">Jenjang Pendidikan & Pilihan Kelas</h2>
                  <p className="text-xs text-slate-400">Materi tersusun rapi sesuai standar Kurikulum Nasional tanpa mencantumkan tahun.</p>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                  {LEVELS.map(lvl => (
                    <div key={lvl.id} className="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 hover:border-teal-500 transition duration-300">
                      <div className="w-12 h-12 rounded-2xl bg-gradient-to-tr from-blue-600 to-teal-500 text-white font-black text-xl flex items-center justify-center mb-4 shadow-md">
                        {lvl.id}
                      </div>
                      <h3 className="font-extrabold text-lg text-white mb-2">{lvl.name}</h3>
                      <p className="text-xs text-slate-400 mb-4">Mencakup {lvl.grades.join(', ')} dengan rangkuman materi lengkap Semester 1 & 2.</p>
                      <button
                        onClick={() => openAuth('register')}
                        className="w-full bg-slate-700 hover:bg-teal-600 text-white font-extrabold text-xs py-2.5 rounded-2xl transition"
                      >
                        Pilih Jenjang {lvl.id}
                      </button>
                    </div>
                  ))}
                </div>
              </section>

            </div>
          )}

          {/* ==================== 2. ARTIKEL ==================== */}
          {landingTab === 'artikel' && (
            <section className="max-w-7xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-teal-400 bg-teal-500/10 px-3 py-1 rounded-full uppercase border border-teal-500/20">Wawasan Akademik</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Artikel & Tips Belajar Terbaru</h2>
                <p className="text-xs text-slate-400">Panduan menguasai pelajaran dan kiat sukses menghadapi ujian sekolah.</p>
              </div>

              <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                {ARTICLES_DATA.map(art => (
                  <div key={art.id} className="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 flex flex-col justify-between hover:border-teal-500 transition">
                    <div>
                      <div className="flex items-center justify-between text-[11px] text-teal-400 font-extrabold mb-3">
                        <span>{art.category}</span>
                        <span className="text-slate-400 font-normal">{art.date} • {art.readTime}</span>
                      </div>
                      <h3 className="font-extrabold text-base text-white mb-2 leading-snug">{art.title}</h3>
                      <p className="text-xs text-slate-300 leading-relaxed mb-4">{art.summary}</p>
                    </div>
                    <button
                      onClick={() => setSelectedArticle(art)}
                      className="w-full bg-slate-700 hover:bg-teal-600 text-white font-extrabold text-xs py-2.5 rounded-2xl transition"
                    >
                      Baca Selengkapnya
                    </button>
                  </div>
                ))}
              </div>
            </section>
          )}

          {/* ==================== 3. KEUNGGULAN ==================== */}
          {landingTab === 'keunggulan' && (
            <section className="max-w-7xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-emerald-400 bg-emerald-500/10 px-3 py-1 rounded-full uppercase border border-emerald-500/20">Mengapa Memilih Kami</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Keunggulan Scientists Learning Center</h2>
                <p className="text-xs text-slate-400">Fasilitas dan modul belajar terpadu dirancang untuk memaksimalkan potensi siswa.</p>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                {ADVANTAGES_DATA.map((adv, idx) => (
                  <div key={idx} className="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 space-y-3 hover:border-emerald-500 transition">
                    <span className="text-3xl">{adv.icon}</span>
                    <h3 className="font-extrabold text-base text-white">{adv.title}</h3>
                    <p className="text-xs text-slate-300 leading-relaxed">{adv.desc}</p>
                  </div>
                ))}
              </div>
            </section>
          )}

          {/* ==================== 4. TESTIMONI ==================== */}
          {landingTab === 'testimoni' && (
            <section className="max-w-7xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-amber-400 bg-amber-500/10 px-3 py-1 rounded-full uppercase border border-amber-500/20">Ulasan Pengguna</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Apa Kata Siswa & Orang Tua</h2>
                <p className="text-xs text-slate-400">Pengalaman nyata berbelajar bersama Scientists Learning Center.</p>
              </div>

              <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                {TESTIMONIALS_DATA.map((t, idx) => (
                  <div key={idx} className="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 space-y-4 hover:border-amber-500 transition">
                    <div className="flex items-center gap-1 text-amber-400">
                      {Array.from({ length: t.rating }).map((_, rIdx) => (
                        <Star key={rIdx} className="w-4 h-4 fill-amber-400" />
                      ))}
                    </div>
                    <p className="text-xs text-slate-200 italic leading-relaxed">"{t.text}"</p>
                    <div className="pt-3 border-t border-slate-700">
                      <h4 className="font-extrabold text-xs text-white">{t.name}</h4>
                      <p className="text-[10px] text-teal-400 font-semibold">{t.role}</p>
                    </div>
                  </div>
                ))}
              </div>
            </section>
          )}

          {/* ==================== 5. FAQ ==================== */}
          {landingTab === 'faq' && (
            <section className="max-w-4xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-blue-400 bg-blue-500/10 px-3 py-1 rounded-full uppercase border border-blue-500/20">Tanya Jawab</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Pertanyaan Sering Diajukan (FAQ)</h2>
                <p className="text-xs text-slate-400">Temukan jawaban lengkap mengenai layanan bimbingan belajar kami.</p>
              </div>

              <div className="space-y-3">
                {FAQS_DATA.map((faq, idx) => (
                  <div key={idx} className="bg-slate-800/80 border border-slate-700/80 rounded-2xl overflow-hidden">
                    <button
                      onClick={() => setOpenFaqIndex(openFaqIndex === idx ? null : idx)}
                      className="w-full p-4 text-left font-extrabold text-xs sm:text-sm text-white flex items-center justify-between gap-4"
                    >
                      <span>{faq.q}</span>
                      <ChevronDown className={`w-4 h-4 text-teal-400 transition transform ${openFaqIndex === idx ? 'rotate-180' : ''}`} />
                    </button>
                    {openFaqIndex === idx && (
                      <div className="p-4 pt-0 text-xs text-slate-300 border-t border-slate-700/50 leading-relaxed bg-slate-900/40">
                        {faq.a}
                      </div>
                    )}
                  </div>
                ))}
              </div>
            </section>
          )}

          {/* ==================== 6. PROMO ==================== */}
          {landingTab === 'promo' && (
            <section className="max-w-5xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-rose-400 bg-rose-500/10 px-3 py-1 rounded-full uppercase border border-rose-500/20">Voucher Spesial</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Promo & Diskon Pendaftaran</h2>
                <p className="text-xs text-slate-400">Gunakan kode voucher di bawah saat mendaftar akun baru.</p>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 gap-6">
                {PROMOS_DATA.map((p, idx) => (
                  <div key={idx} className="bg-gradient-to-br from-slate-800 via-slate-800 to-teal-950 border border-teal-500/40 rounded-3xl p-6 space-y-4 shadow-lg">
                    <div className="flex items-center justify-between">
                      <span className="bg-rose-500 text-white font-black text-xs px-3 py-1 rounded-full uppercase">{p.discount}</span>
                      <span className="text-[10px] text-slate-400 font-semibold">{p.valid}</span>
                    </div>
                    <h3 className="font-extrabold text-base text-white">{p.desc}</h3>
                    <div className="bg-slate-900 border border-dashed border-teal-400 p-3 rounded-2xl flex items-center justify-between">
                      <span className="font-mono text-xs font-black text-teal-300">{p.code}</span>
                      <button
                        onClick={() => {
                          setCopiedCode(p.code);
                          setTimeout(() => setCopiedCode(''), 2000);
                        }}
                        className="bg-teal-600 hover:bg-teal-500 text-white text-[11px] font-bold px-3 py-1.5 rounded-xl transition"
                      >
                        {copiedCode === p.code ? 'Terklaim!' : 'Klaim Kode'}
                      </button>
                    </div>
                  </div>
                ))}
              </div>
            </section>
          )}

          {/* ==================== 7. LOWONGAN ==================== */}
          {landingTab === 'lowongan' && (
            <section className="max-w-5xl mx-auto px-4 sm:px-6 py-12 space-y-8">
              <div className="text-center space-y-2">
                <span className="text-xs font-black text-indigo-400 bg-indigo-500/10 px-3 py-1 rounded-full uppercase border border-indigo-500/20">Karir & Edukator</span>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Lowongan Pengajar & Staff Bimbel</h2>
                <p className="text-xs text-slate-400">Bergabunglah menjadi bagian dari tim pengajar Scientists Learning Center.</p>
              </div>

              <div className="space-y-4">
                {VACANCIES_DATA.map((vac, idx) => (
                  <div key={idx} className="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 flex flex-wrap items-center justify-between gap-4 hover:border-indigo-500 transition">
                    <div className="space-y-1 max-w-xl">
                      <div className="flex items-center gap-2">
                        <span className="bg-indigo-500/20 text-indigo-300 font-extrabold text-[10px] px-2.5 py-0.5 rounded-full border border-indigo-500/30">{vac.type}</span>
                        <span className="text-[10px] text-slate-400 font-semibold">{vac.loc}</span>
                      </div>
                      <h3 className="font-extrabold text-base text-white">{vac.title}</h3>
                      <p className="text-xs text-slate-300 leading-relaxed">{vac.req}</p>
                    </div>

                    <button
                      onClick={() => { setSelectedJob(vac); setJobAppliedSuccess(false); }}
                      className="bg-gradient-to-r from-teal-500 to-indigo-600 hover:from-teal-600 hover:to-indigo-700 text-white font-extrabold text-xs px-5 py-2.5 rounded-2xl shadow-md transition"
                    >
                      Kirim Lamaran
                    </button>
                  </div>
                ))}
              </div>
            </section>
          )}

        </main>

        {/* PUBLIC FOOTER */}
        <footer className="bg-slate-950 border-t border-slate-800 py-8">
          <div className="max-w-7xl mx-auto px-4 text-center text-xs text-slate-400 space-y-2">
            <div className="flex items-center justify-center gap-2 text-white font-black text-sm">
              <GraduationCap className="w-5 h-5 text-teal-400" /> Scientists Learning Center
            </div>
            <p className="font-semibold text-slate-300">
              Platform Bimbingan Belajar Terpadu SD (1-6), SMP (7-9), & SMA (10-12) Berstandar Kurikulum Nasional.
            </p>
            <p className="text-[11px] text-slate-500">
              Hak Cipta Dilindungi © Scientists Learning Center.
            </p>
          </div>
        </footer>

        {/* ========================================== */}
        {/* MODAL AUTHENTICATION (LOGIN / REGISTER / FORGOT) */}
        {/* ========================================== */}
        {authModalOpen && (
          <div className="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm flex items-center justify-center p-4">
            <div className="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl relative text-slate-800 border border-slate-100 animate-in fade-in zoom-in duration-200">
              
              <button
                onClick={() => setAuthModalOpen(false)}
                className="absolute top-4 right-4 text-slate-400 hover:text-slate-700 p-1.5 rounded-full hover:bg-slate-100"
              >
                <X className="w-5 h-5" />
              </button>

              {/* Header inside modal */}
              <div className="text-center mb-6">
                <div className="w-14 h-14 rounded-2xl bg-gradient-to-tr from-blue-900 to-teal-500 text-white flex items-center justify-center mx-auto mb-2 shadow-md">
                  <GraduationCap className="w-8 h-8" />
                </div>
                <h3 className="font-black text-xl text-blue-950">Scientists Learning Center</h3>
                <p className="text-xs text-slate-500 mt-0.5">Akses Seluruh Modul & Formatif 1-10</p>
              </div>

              {/* Notification Alert */}
              {authNotification && (
                <div className={`mb-4 p-3 rounded-2xl text-xs font-semibold flex items-center gap-2 ${
                  authNotification.type === 'error' ? 'bg-rose-50 text-rose-700 border border-rose-200' : 'bg-emerald-50 text-emerald-700 border border-emerald-200'
                }`}>
                  <AlertCircle className="w-4 h-4 shrink-0" />
                  <span>{authNotification.text}</span>
                </div>
              )}

              {/* GOOGLE SIGN IN BUTTON */}
              {authView !== 'forgot' && (
                <div className="mb-5">
                  <button
                    type="button"
                    onClick={handleGoogleLoginMock}
                    className="w-full flex items-center justify-center gap-3 bg-white hover:bg-slate-50 border border-slate-300 text-slate-700 font-bold text-xs py-2.5 px-4 rounded-2xl shadow-sm transition"
                  >
                    <svg className="w-5 h-5" viewBox="0 0 24 24">
                      <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                      <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                      <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/>
                      <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/>
                    </svg>
                    Masuk dengan Akun Google
                  </button>
                  <div className="relative my-4">
                    <div className="absolute inset-0 flex items-center"><div className="w-full border-t border-slate-200"></div></div>
                    <div className="relative flex justify-center text-[10px] uppercase tracking-wider font-extrabold text-slate-400"><span className="bg-white px-3">atau</span></div>
                  </div>
                </div>
              )}

              {/* FORM LOGIN */}
              {authView === 'login' && (
                <form onSubmit={handleLoginSubmit} className="space-y-3.5">
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">Username / Email Siswa</label>
                    <input
                      type="text"
                      required
                      placeholder="Masukkan username/email"
                      value={authForm.username}
                      onChange={(e) => setAuthForm({ ...authForm, username: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-teal-500"
                    />
                  </div>

                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">Password</label>
                    <input
                      type="password"
                      required
                      placeholder="••••••••"
                      value={authForm.password}
                      onChange={(e) => setAuthForm({ ...authForm, password: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-teal-500"
                    />
                  </div>

                  <div className="flex justify-end">
                    <button
                      type="button"
                      onClick={() => setAuthView('forgot')}
                      className="text-xs font-bold text-teal-600 hover:underline"
                    >
                      Lupa Password?
                    </button>
                  </div>

                  <button
                    type="submit"
                    className="w-full bg-gradient-to-r from-blue-900 to-teal-700 hover:from-blue-950 hover:to-teal-800 text-white font-extrabold py-2.5 rounded-2xl shadow-md text-xs"
                  >
                    MASUK SEKARANG
                  </button>

                  <div className="text-center text-xs text-slate-600 pt-1">
                    Belum punya akun?{' '}
                    <button
                      type="button"
                      onClick={() => setAuthView('register')}
                      className="font-extrabold text-teal-600 hover:underline"
                    >
                      Buat Akun Baru
                    </button>
                  </div>
                </form>
              )}

              {/* FORM REGISTER */}
              {authView === 'register' && (
                <form onSubmit={handleRegisterSubmit} className="space-y-3">
                  <div>
                    <label className="block text-[11px] font-bold text-slate-700 mb-1">Username Unik</label>
                    <input
                      type="text"
                      required
                      placeholder="username"
                      value={authForm.username}
                      onChange={(e) => setAuthForm({ ...authForm, username: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold"
                    />
                  </div>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-700 mb-1">Biodata Nama Lengkap Siswa</label>
                    <input
                      type="text"
                      required
                      placeholder="Nama Sesuai Raport"
                      value={authForm.fullName}
                      onChange={(e) => setAuthForm({ ...authForm, fullName: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold"
                    />
                  </div>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-700 mb-1">Email Aktif</label>
                    <input
                      type="email"
                      required
                      placeholder="email@ domain.com"
                      value={authForm.email}
                      onChange={(e) => setAuthForm({ ...authForm, email: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold"
                    />
                  </div>

                  <div className="grid grid-cols-2 gap-2">
                    <div>
                      <label className="block text-[11px] font-bold text-slate-700 mb-1">Jenjang</label>
                      <select
                        value={authForm.level}
                        onChange={(e) => {
                          const lvl = e.target.value;
                          const defaultGrade = LEVELS.find(l => l.id === lvl).grades[0];
                          setAuthForm({ ...authForm, level: lvl, grade: defaultGrade });
                        }}
                        className="w-full px-2 py-2 bg-slate-50 border rounded-xl text-xs font-semibold"
                      >
                        {LEVELS.map(l => <option key={l.id} value={l.id}>{l.name}</option>)}
                      </select>
                    </div>
                    <div>
                      <label className="block text-[11px] font-bold text-slate-700 mb-1">Kelas</label>
                      <select
                        value={authForm.grade}
                        onChange={(e) => setAuthForm({ ...authForm, grade: e.target.value })}
                        className="w-full px-2 py-2 bg-slate-50 border rounded-xl text-xs font-semibold"
                      >
                        {LEVELS.find(l => l.id === authForm.level)?.grades.map(g => (
                          <option key={g} value={g}>{g}</option>
                        ))}
                      </select>
                    </div>
                  </div>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-700 mb-1">Password Baru</label>
                    <input
                      type="password"
                      required
                      placeholder="••••••••"
                      value={authForm.password}
                      onChange={(e) => setAuthForm({ ...authForm, password: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold"
                    />
                  </div>

                  <button
                    type="submit"
                    className="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-2.5 rounded-2xl text-xs shadow-md mt-1"
                  >
                    BUAT AKUN BARU
                  </button>

                  <div className="text-center text-xs text-slate-600 pt-1">
                    Sudah punya akun?{' '}
                    <button
                      type="button"
                      onClick={() => setAuthView('login')}
                      className="font-extrabold text-teal-600 hover:underline"
                    >
                      Masuk di Sini
                    </button>
                  </div>
                </form>
              )}

              {/* FORM FORGOT */}
              {authView === 'forgot' && (
                <form onSubmit={handleForgotSubmit} className="space-y-4">
                  <div className="text-center space-y-1">
                    <h4 className="font-bold text-sm text-blue-950">Pemulihan Password</h4>
                    <p className="text-[11px] text-slate-500">Masukkan email Anda untuk menerima instruksi reset.</p>
                  </div>

                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">Email Terdaftar</label>
                    <input
                      type="email"
                      required
                      placeholder="email@ domain.com"
                      value={authForm.email}
                      onChange={(e) => setAuthForm({ ...authForm, email: e.target.value })}
                      className="w-full px-3 py-2 bg-slate-50 border rounded-xl text-xs font-semibold"
                    />
                  </div>

                  <button
                    type="submit"
                    className="w-full bg-blue-900 text-white font-bold py-2.5 rounded-2xl text-xs"
                  >
                    KIRIM PETUNJUK RESET
                  </button>

                  <button
                    type="button"
                    onClick={() => setAuthView('login')}
                    className="w-full text-xs font-bold text-slate-500 hover:text-slate-800"
                  >
                    Kembali ke Form Login
                  </button>
                </form>
              )}

            </div>
          </div>
        )}

        {/* MODAL ARTIKEL READER */}
        {selectedArticle && (
          <div className="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm flex items-center justify-center p-4">
            <div className="bg-slate-900 border border-slate-700 rounded-3xl max-w-xl w-full p-6 text-white relative">
              <button onClick={() => setSelectedArticle(null)} className="absolute top-4 right-4 text-slate-400 hover:text-white">
                <X className="w-5 h-5" />
              </button>
              <span className="text-[10px] bg-teal-500/20 text-teal-300 font-extrabold px-2.5 py-1 rounded-full uppercase border border-teal-500/30">
                {selectedArticle.category}
              </span>
              <h3 className="font-extrabold text-lg text-white mt-3 mb-2">{selectedArticle.title}</h3>
              <p className="text-xs text-slate-400 mb-4">{selectedArticle.date} • {selectedArticle.readTime}</p>
              <p className="text-xs text-slate-200 leading-relaxed bg-slate-800/80 p-4 rounded-2xl border border-slate-700 mb-4">
                {selectedArticle.content}
              </p>
              <button
                onClick={() => setSelectedArticle(null)}
                className="w-full bg-teal-600 hover:bg-teal-500 text-white font-bold text-xs py-2.5 rounded-xl"
              >
                Tutup Artikel
              </button>
            </div>
          </div>
        )}

        {/* MODAL LOWONGAN JOB APPLICATION */}
        {selectedJob && (
          <div className="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm flex items-center justify-center p-4">
            <div className="bg-slate-900 border border-indigo-500/30 rounded-3xl max-w-md w-full p-6 text-white relative">
              <button onClick={() => setSelectedJob(null)} className="absolute top-4 right-4 text-slate-400 hover:text-white">
                <X className="w-5 h-5" />
              </button>

              {!jobAppliedSuccess ? (
                <form onSubmit={(e) => { e.preventDefault(); setJobAppliedSuccess(true); }} className="space-y-3.5">
                  <h3 className="font-extrabold text-base text-white">Form Lamaran: {selectedJob.title}</h3>
                  <p className="text-xs text-slate-400">{selectedJob.type} • {selectedJob.loc}</p>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-300 mb-1">Nama Lengkap</label>
                    <input type="text" required placeholder="Sesuai KTP/Ijazah" className="w-full bg-slate-800 border border-slate-700 rounded-xl text-xs p-2.5 text-white" />
                  </div>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-300 mb-1">Email & WhatsApp</label>
                    <input type="text" required placeholder="0812... / email@ domain.com" className="w-full bg-slate-800 border border-slate-700 rounded-xl text-xs p-2.5 text-white" />
                  </div>

                  <div>
                    <label className="block text-[11px] font-bold text-slate-300 mb-1">Link CV / Portofolio (Google Drive)</label>
                    <input type="url" required placeholder="https://drive.google.com/..." className="w-full bg-slate-800 border border-slate-700 rounded-xl text-xs p-2.5 text-white" />
                  </div>

                  <button type="submit" className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold text-xs py-2.5 rounded-2xl shadow-md">
                    KIRIM BERKAS LAMARAN
                  </button>
                </form>
              ) : (
                <div className="text-center space-y-3 py-4">
                  <CheckCircle className="w-12 h-12 text-emerald-400 mx-auto" />
                  <h4 className="font-extrabold text-base text-white">Lamaran Berhasil Terkirim!</h4>
                  <p className="text-xs text-slate-300">Tim HR Scientists Learning Center akan mengontak Anda melalui WhatsApp/Email.</p>
                  <button onClick={() => setSelectedJob(null)} className="w-full bg-slate-800 text-white font-bold text-xs py-2 rounded-xl">
                    Tutup Window
                  </button>
                </div>
              )}
            </div>
          </div>
        )}

      </div>
    );
  }

  // ==========================================
  // VIEW 2: AUTHENTICATED STUDENT DASHBOARD
  // ==========================================
  return (
    <div className="min-h-screen bg-slate-100 flex flex-col font-sans">
      
      {/* INTERNAL TOP HEADER */}
      <header className="bg-gradient-to-r from-blue-950 via-blue-900 to-teal-800 text-white sticky top-0 z-50 shadow-lg">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 py-3 flex flex-wrap items-center justify-between gap-4">
          
          {/* Brand Logo */}
          <div className="flex items-center gap-3">
            <div className="w-10 h-10 rounded-2xl bg-gradient-to-tr from-emerald-400 to-teal-500 text-slate-950 flex items-center justify-center font-black text-xl shadow-md">
              <GraduationCap className="w-6 h-6 text-white" />
            </div>
            <div>
              <h1 className="font-black text-base sm:text-lg text-white">Scientists Learning Center</h1>
              <p className="text-[10px] text-emerald-300 font-semibold">Platform Bimbingan Belajar Kurikulum Nasional</p>
            </div>
          </div>

          {/* Level Switcher */}
          <div className="flex items-center gap-1 bg-blue-950/70 p-1 rounded-2xl border border-blue-700/50">
            {LEVELS.map(lvl => (
              <button
                key={lvl.id}
                onClick={() => setSelectedLevel(lvl.id)}
                className={`px-3 py-1 rounded-xl text-xs font-bold transition ${
                  selectedLevel === lvl.id ? 'bg-gradient-to-r from-teal-500 to-emerald-500 text-white shadow' : 'text-blue-100 hover:bg-blue-800/50'
                }`}
              >
                {lvl.id}
              </button>
            ))}
          </div>

          {/* User Widget */}
          <div className="flex items-center gap-3 border-l border-blue-800/80 pl-4">
            <div className="text-right hidden sm:block">
              <p className="text-xs font-extrabold text-white">{currentUser.fullName}</p>
              <p className="text-[10px] text-emerald-300 font-semibold">{selectedLevel} • {selectedGrade}</p>
            </div>
            <div className="w-9 h-9 rounded-full bg-teal-500 text-white flex items-center justify-center text-base font-bold shadow-md">
              {currentUser.avatar}
            </div>
            <button
              onClick={handleLogout}
              title="Log Out"
              className="p-2 rounded-xl bg-rose-600/80 hover:bg-rose-600 text-white transition flex items-center gap-1 text-xs font-bold"
            >
              <LogOut className="w-3.5 h-3.5" /> <span className="hidden md:inline">Keluar</span>
            </button>
          </div>

        </div>
      </header>

      {/* SUB-HEADER / GRADE & SEARCH BAR */}
      <div className="bg-white border-b border-slate-200 shadow-sm py-2 px-4 sm:px-6">
        <div className="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-3">
          
          {/* Grade Pills */}
          <div className="flex items-center gap-2 overflow-x-auto py-1">
            <span className="text-xs font-bold text-slate-500 uppercase tracking-wider whitespace-nowrap">Pilih Kelas:</span>
            {LEVELS.find(l => l.id === selectedLevel)?.grades.map(grd => (
              <button
                key={grd}
                onClick={() => setSelectedGrade(grd)}
                className={`px-3 py-1 rounded-full text-xs font-bold transition whitespace-nowrap ${
                  selectedGrade === grd ? 'bg-gradient-to-r from-blue-900 to-teal-700 text-white shadow-sm' : 'bg-slate-100 text-slate-600 hover:bg-slate-200'
                }`}
              >
                {grd}
              </button>
            ))}
          </div>

          {/* Subject Search */}
          <div className="relative w-full sm:w-64">
            <Search className="w-4 h-4 absolute left-3 top-2.5 text-slate-400" />
            <input
              type="text"
              placeholder="Cari Mata Pelajaran..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="w-full pl-9 pr-3 py-1.5 bg-slate-100 rounded-xl text-xs font-medium border border-transparent focus:border-teal-500 focus:bg-white focus:outline-none transition"
            />
          </div>

        </div>
      </div>

      {/* MAIN NAVIGATION TAB BAR (THE 4 PILLARS) */}
      <div className="bg-gradient-to-r from-blue-900 to-teal-800 text-white shadow-inner">
        <div className="max-w-7xl mx-auto px-4 flex space-x-1 overflow-x-auto">
          
          <button
            onClick={() => { setActiveTab('pembelajaran'); setSelectedFormativeNum(null); }}
            className={`py-3.5 px-5 font-bold text-xs sm:text-sm flex items-center gap-2 border-b-4 transition whitespace-nowrap ${
              activeTab === 'pembelajaran' ? 'border-emerald-400 text-emerald-300 bg-white/10' : 'border-transparent text-blue-100 hover:bg-white/5'
            }`}
          >
            <BookOpen className="w-4 h-4" /> 1. Pembelajaran & Penyampaian Materi
          </button>

          <button
            onClick={() => setActiveTab('evaluasi')}
            className={`py-3.5 px-5 font-bold text-xs sm:text-sm flex items-center gap-2 border-b-4 transition whitespace-nowrap ${
              activeTab === 'evaluasi' ? 'border-emerald-400 text-emerald-300 bg-white/10' : 'border-transparent text-blue-100 hover:bg-white/5'
            }`}
          >
            <Award className="w-4 h-4" /> 2. Evaluasi & Asesmen (Formatif 1-10)
          </button>

          <button
            onClick={() => { setActiveTab('interaksi'); setSelectedFormativeNum(null); }}
            className={`py-3.5 px-5 font-bold text-xs sm:text-sm flex items-center gap-2 border-b-4 transition whitespace-nowrap ${
              activeTab === 'interaksi' ? 'border-emerald-400 text-emerald-300 bg-white/10' : 'border-transparent text-blue-100 hover:bg-white/5'
            }`}
          >
            <MessageSquare className="w-4 h-4" /> 3. Interaksi & Dukungan Belajar
          </button>

          <button
            onClick={() => { setActiveTab('manajemen'); setSelectedFormativeNum(null); }}
            className={`py-3.5 px-5 font-bold text-xs sm:text-sm flex items-center gap-2 border-b-4 transition whitespace-nowrap ${
              activeTab === 'manajemen' ? 'border-emerald-400 text-emerald-300 bg-white/10' : 'border-transparent text-blue-100 hover:bg-white/5'
            }`}
          >
            <UserCheck className="w-4 h-4" /> 4. Manajemen & Administrasi
          </button>

        </div>
      </div>

      {/* DASHBOARD BODY */}
      <main className="max-w-7xl mx-auto px-4 sm:px-6 py-6 flex-grow w-full">
        
        {/* PILAR 1: PEMBELAJARAN & PENYAMPAIAN MATERI */}
        {activeTab === 'pembelajaran' && (
          <div className="grid grid-cols-1 lg:grid-cols-4 gap-6">
            
            {/* Subject List Sidebar */}
            <div className="lg:col-span-1 bg-white rounded-3xl shadow-sm border border-slate-200 p-4 h-fit">
              <h3 className="font-extrabold text-xs text-blue-950 uppercase tracking-wider mb-3 pb-2 border-b flex items-center justify-between">
                <span>Pelajaran {selectedLevel}</span>
                <span className="bg-teal-100 text-teal-800 px-2 py-0.5 rounded-full text-[10px]">{filteredSubjectsList.length} Mapel</span>
              </h3>
              
              <div className="space-y-1.5 max-h-[500px] overflow-y-auto pr-1">
                {filteredSubjectsList.map((sub) => (
                  <button
                    key={sub.id}
                    onClick={() => setSelectedSubject(sub)}
                    className={`w-full flex items-center justify-between p-2.5 rounded-2xl text-xs font-bold text-left transition ${
                      selectedSubject.id === sub.id ? 'bg-gradient-to-r from-blue-900 to-teal-700 text-white shadow' : 'text-slate-700 hover:bg-slate-100'
                    }`}
                  >
                    <span className="flex items-center gap-2 truncate">
                      <span>{sub.icon}</span>
                      <span className="truncate">{sub.name}</span>
                    </span>
                    <ChevronRight className="w-3.5 h-3.5 shrink-0 opacity-70" />
                  </button>
                ))}
              </div>
            </div>

            {/* Material Summary Content */}
            <div className="lg:col-span-3 space-y-6">
              
              <div className="bg-gradient-to-r from-blue-900 via-teal-800 to-emerald-700 rounded-3xl p-6 text-white shadow-xl flex flex-wrap items-center justify-between gap-4">
                <div>
                  <span className="inline-block px-3 py-1 bg-white/20 rounded-full text-xs font-extrabold mb-2 backdrop-blur-md">
                    {selectedLevel} • {selectedGrade}
                  </span>
                  <h2 className="text-2xl font-black flex items-center gap-3">
                    <span className="text-3xl">{selectedSubject.icon}</span> {selectedSubject.name}
                  </h2>
                  <p className="text-xs text-teal-100 mt-1 max-w-xl">
                    Rangkuman Materi & Modul Lengkap Berstandar Kurikulum Nasional Semester 1 dan Semester 2.
                  </p>
                </div>
              </div>

              {/* SEMESTER 1 */}
              <div className="bg-white rounded-3xl p-6 border border-slate-200 shadow-sm space-y-4">
                <div className="flex items-center justify-between border-b pb-3">
                  <h3 className="font-extrabold text-base text-blue-950 flex items-center gap-2">
                    <span className="w-3 h-3 rounded-full bg-blue-600"></span> Semester 1 (Ganjil)
                  </h3>
                  <span className="text-xs bg-blue-50 text-blue-700 font-bold px-3 py-1 rounded-full">Bab 1 - 3</span>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
                  {generateDetailedMaterials(selectedSubject.name, selectedGrade).sem1.map((item) => (
                    <div key={item.bab} className="bg-slate-50 border border-slate-200 rounded-2xl p-4 hover:border-teal-400 hover:shadow transition flex flex-col justify-between">
                      <div>
                        <span className="text-[10px] font-bold bg-teal-50 text-teal-700 px-2 py-0.5 rounded border border-teal-200 mb-2 inline-block">Bab {item.bab}</span>
                        <h4 className="font-bold text-xs text-slate-800 mb-2 leading-snug">{item.title}</h4>
                        <p className="text-[11px] text-slate-600 leading-relaxed mb-3">{item.summary}</p>
                      </div>
                      <div className="pt-2 border-t border-slate-200/60 flex items-center justify-between">
                        <button className="text-[11px] font-bold text-teal-600 flex items-center gap-1"><PlayCircle className="w-3.5 h-3.5" /> Video Modul</button>
                        <button className="text-[11px] font-bold text-blue-900 flex items-center gap-1"><Download className="w-3.5 h-3.5" /> Unduh PDF</button>
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              {/* SEMESTER 2 */}
              <div className="bg-white rounded-3xl p-6 border border-slate-200 shadow-sm space-y-4">
                <div className="flex items-center justify-between border-b pb-3">
                  <h3 className="font-extrabold text-base text-blue-950 flex items-center gap-2">
                    <span className="w-3 h-3 rounded-full bg-emerald-600"></span> Semester 2 (Genap)
                  </h3>
                  <span className="text-xs bg-emerald-50 text-emerald-700 font-bold px-3 py-1 rounded-full">Bab 4 - 6</span>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
                  {generateDetailedMaterials(selectedSubject.name, selectedGrade).sem2.map((item) => (
                    <div key={item.bab} className="bg-slate-50 border border-slate-200 rounded-2xl p-4 hover:border-emerald-400 hover:shadow transition flex flex-col justify-between">
                      <div>
                        <span className="text-[10px] font-bold bg-emerald-50 text-emerald-700 px-2 py-0.5 rounded border border-emerald-200 mb-2 inline-block">Bab {item.bab}</span>
                        <h4 className="font-bold text-xs text-slate-800 mb-2 leading-snug">{item.title}</h4>
                        <p className="text-[11px] text-slate-600 leading-relaxed mb-3">{item.summary}</p>
                      </div>
                      <div className="pt-2 border-t border-slate-200/60 flex items-center justify-between">
                        <button className="text-[11px] font-bold text-emerald-600 flex items-center gap-1"><PlayCircle className="w-3.5 h-3.5" /> Video Modul</button>
                        <button className="text-[11px] font-bold text-blue-900 flex items-center gap-1"><Download className="w-3.5 h-3.5" /> Unduh PDF</button>
                      </div>
                    </div>
                  ))}
                </div>
              </div>

            </div>

          </div>
        )}

        {/* PILAR 2: EVALUASI & ASESMEN (FORMATIF 1-10) */}
        {activeTab === 'evaluasi' && (
          <div className="space-y-6">
            
            <div className="bg-white rounded-3xl p-6 border border-slate-200 shadow-sm flex flex-wrap items-center justify-between gap-4">
              <div>
                <span className="text-[10px] font-black text-teal-700 bg-teal-50 px-3 py-1 rounded-full border border-teal-200 uppercase">Uji Formatif</span>
                <h2 className="text-xl font-extrabold text-blue-950 mt-2 flex items-center gap-2">
                  <span>{selectedSubject.icon}</span> Evaluasi Formatif {selectedSubject.name} ({selectedLevel} {selectedGrade})
                </h2>
                <p className="text-xs text-slate-500 mt-1">10 Urutan Formatif (Masing-masing 20 soal interaktif, 20 menit, dan kunci pembahasan).</p>
              </div>

              <select
                value={selectedSubject.id}
                onChange={(e) => {
                  const sub = SUBJECTS_LIST.find(s => s.id === e.target.value);
                  if (sub) { setSelectedSubject(sub); setSelectedFormativeNum(null); }
                }}
                className="bg-slate-50 border border-slate-300 text-slate-800 font-bold text-xs rounded-xl p-2.5 focus:outline-none"
              >
                {filteredSubjectsList.map(sub => (
                  <option key={sub.id} value={sub.id}>{sub.name}</option>
                ))}
              </select>
            </div>

            {/* FORMATIF GRID 1-10 */}
            {!selectedFormativeNum && (
              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
                {Array.from({ length: 10 }, (_, i) => i + 1).map((num) => (
                  <div key={num} className="bg-white border border-slate-200 rounded-3xl p-5 hover:border-teal-500 hover:shadow-xl transition flex flex-col justify-between">
                    <div>
                      <div className="w-12 h-12 rounded-2xl bg-gradient-to-tr from-blue-950 to-teal-700 text-white font-black text-lg flex items-center justify-center mx-auto mb-3 shadow">
                        F{num}
                      </div>
                      <h4 className="font-extrabold text-slate-800 text-sm text-center">Formatif {num}</h4>
                      <p className="text-[11px] text-slate-500 text-center mt-1">20 Soal • 20 Menit</p>
                    </div>
                    <button
                      onClick={() => startQuiz(num)}
                      className="mt-4 w-full bg-slate-900 hover:bg-teal-700 text-white font-extrabold text-xs py-2.5 rounded-2xl transition"
                    >
                      Mulai Formatif {num}
                    </button>
                  </div>
                ))}
              </div>
            )}

            {/* QUIZ INTERFACE */}
            {selectedFormativeNum && (
              <div className="bg-white rounded-3xl border border-slate-200 shadow-xl p-6 space-y-6">
                
                <div className="flex flex-wrap items-center justify-between border-b pb-4 gap-4">
                  <div>
                    <button onClick={() => setSelectedFormativeNum(null)} className="text-xs text-slate-500 font-bold hover:text-slate-800 flex items-center gap-1 mb-1">
                      <ArrowLeft className="w-3.5 h-3.5" /> Kembali
                    </button>
                    <h3 className="font-black text-lg text-blue-950">Formatif {selectedFormativeNum} - {selectedSubject.name}</h3>
                  </div>

                  <div className="flex items-center gap-3">
                    <div className="flex items-center gap-2 bg-amber-50 text-amber-800 border border-amber-200 px-3.5 py-1.5 rounded-2xl font-mono text-xs font-black">
                      <Clock className="w-4 h-4 text-amber-600" />
                      <span>{Math.floor(quizTimer / 60)}:{(quizTimer % 60).toString().padStart(2, '0')}</span>
                    </div>

                    {!quizSubmitted ? (
                      <button onClick={() => setQuizSubmitted(true)} className="bg-emerald-600 text-white font-black text-xs py-2 px-4 rounded-2xl shadow">
                        Kumpulkan
                      </button>
                    ) : (
                      <div className="bg-gradient-to-r from-blue-900 to-teal-800 text-white px-5 py-2 rounded-2xl text-center shadow">
                        <span className="text-[9px] block uppercase text-teal-300 font-bold">Skor</span>
                        <span className="text-xl font-black">{calculateScore(generate20FormativeQuestions(selectedSubject.name, selectedFormativeNum))} / 100</span>
                      </div>
                    )}
                  </div>
                </div>

                {/* Question Grid 1-20 */}
                <div className="bg-slate-50 p-4 rounded-2xl border border-slate-200">
                  <span className="text-[11px] font-bold text-slate-600 block mb-2">Nomor Soal (1 - 20):</span>
                  <div className="flex flex-wrap gap-2">
                    {generate20FormativeQuestions(selectedSubject.name, selectedFormativeNum).map((q, idx) => {
                      const isAnswered = quizAnswers[q.id] !== undefined;
                      const isCurrent = currentQuestionIndex === idx;
                      return (
                        <button
                          key={q.id}
                          onClick={() => setCurrentQuestionIndex(idx)}
                          className={`w-8 h-8 rounded-xl font-black text-xs transition border ${
                            isCurrent ? 'ring-2 ring-teal-500 bg-blue-900 text-white' : isAnswered ? 'bg-teal-600 text-white' : 'bg-white text-slate-700'
                          }`}
                        >
                          {q.id}
                        </button>
                      );
                    })}
                  </div>
                </div>

                {/* Active Question */}
                {(() => {
                  const questions = generate20FormativeQuestions(selectedSubject.name, selectedFormativeNum);
                  const q = questions[currentQuestionIndex];
                  const userAns = quizAnswers[q.id];

                  return (
                    <div className="p-6 rounded-2xl bg-white border border-slate-200 shadow-sm space-y-4">
                      <h4 className="font-extrabold text-sm text-slate-800 leading-relaxed">{q.id}. {q.question}</h4>

                      <div className="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        {q.options.map((opt, oIdx) => {
                          let style = 'bg-slate-50 border-slate-200 text-slate-700 hover:bg-slate-100';
                          if (userAns === oIdx) style = 'bg-blue-900 text-white border-blue-900 font-bold';
                          if (quizSubmitted) {
                            if (oIdx === q.correctAnswer) style = 'bg-emerald-600 text-white border-emerald-600 font-bold';
                            else if (userAns === oIdx) style = 'bg-rose-600 text-white border-rose-600';
                          }

                          return (
                            <button
                              key={oIdx}
                              disabled={quizSubmitted}
                              onClick={() => setQuizAnswers({ ...quizAnswers, [q.id]: oIdx })}
                              className={`text-left p-3.5 rounded-2xl border text-xs transition flex items-center justify-between ${style}`}
                            >
                              <span>{opt}</span>
                            </button>
                          );
                        })}
                      </div>

                      {quizSubmitted && (
                        <div className="p-4 rounded-2xl bg-blue-50 border border-blue-200 text-xs text-blue-950 space-y-1">
                          <span className="font-extrabold text-blue-900 flex items-center gap-1">
                            <Info className="w-4 h-4 text-teal-600" /> Kunci Pembahasan Resmi:
                          </span>
                          <p className="leading-relaxed pl-5">{q.explanation}</p>
                        </div>
                      )}

                      <div className="flex items-center justify-between pt-4 border-t">
                        <button disabled={currentQuestionIndex === 0} onClick={() => setCurrentQuestionIndex(prev => prev - 1)} className="px-4 py-2 border rounded-xl text-xs font-bold disabled:opacity-40">Sebelumnya</button>
                        <span className="text-xs text-slate-500 font-semibold">Soal {currentQuestionIndex + 1} / 20</span>
                        <button disabled={currentQuestionIndex === questions.length - 1} onClick={() => setCurrentQuestionIndex(prev => prev + 1)} className="px-4 py-2 bg-blue-900 text-white rounded-xl text-xs font-bold disabled:opacity-40">Selanjutnya</button>
                      </div>
                    </div>
                  );
                })()}

              </div>
            )}

          </div>
        )}

        {/* PILAR 3: INTERAKSI & DUKUNGAN BELAJAR */}
        {activeTab === 'interaksi' && (
          <div className="space-y-6">
            <div className="flex items-center gap-2 border-b pb-3">
              <button onClick={() => setActiveSubInteraksi('forum')} className={`px-4 py-2 rounded-2xl text-xs font-extrabold ${activeSubInteraksi === 'forum' ? 'bg-teal-600 text-white' : 'bg-white text-slate-600'}`}>Forum Diskusi PR</button>
              <button onClick={() => setActiveSubInteraksi('chat')} className={`px-4 py-2 rounded-2xl text-xs font-extrabold ${activeSubInteraksi === 'chat' ? 'bg-teal-600 text-white' : 'bg-white text-slate-600'}`}>Live Consultation Chat</button>
            </div>

            {activeSubInteraksi === 'forum' && (
              <div className="space-y-4">
                <div className="bg-white rounded-3xl p-5 border shadow-sm space-y-3">
                  <h3 className="font-extrabold text-sm text-blue-950 flex items-center gap-2"><MessageSquare className="w-4 h-4 text-teal-600" /> Ajukan Pertanyaan ke Forum</h3>
                  <div className="grid grid-cols-1 sm:grid-cols-3 gap-2">
                    <select value={newPost.subject} onChange={(e) => setNewPost({ ...newPost, subject: e.target.value })} className="bg-slate-50 border text-xs rounded-xl p-2.5 font-semibold">
                      {SUBJECTS_LIST.map(s => <option key={s.id} value={s.name}>{s.name}</option>)}
                    </select>
                    <input type="text" placeholder="Tuliskan topik/pertanyaan PR..." value={newPost.title} onChange={(e) => setNewPost({ ...newPost, title: e.target.value })} className="sm:col-span-2 bg-slate-50 border text-xs rounded-xl p-2.5 font-semibold" />
                  </div>
                  <button onClick={() => {
                    if (!newPost.title) return;
                    setDiscussions([{ id: Date.now(), user: currentUser.fullName, grade: `${selectedLevel} ${selectedGrade}`, subject: newPost.subject, title: newPost.title, replies: 0, time: 'Baru saja' }, ...discussions]);
                    setNewPost({ subject: 'Matematika', title: '' });
                  }} className="w-full bg-teal-600 text-white font-bold text-xs py-2.5 rounded-2xl">Kirim Pertanyaan</button>
                </div>

                {discussions.map(disc => (
                  <div key={disc.id} className="bg-white rounded-3xl p-5 border shadow-sm space-y-2">
                    <div className="flex items-center justify-between text-xs text-slate-500">
                      <span className="font-bold text-blue-950">{disc.user} ({disc.grade})</span>
                      <span>{disc.time}</span>
                    </div>
                    <span className="inline-block bg-teal-50 text-teal-800 font-bold px-2.5 py-0.5 rounded-full text-[10px]">{disc.subject}</span>
                    <h4 className="font-bold text-slate-800 text-sm">{disc.title}</h4>
                  </div>
                ))}
              </div>
            )}

            {activeSubInteraksi === 'chat' && (
              <div className="bg-white rounded-3xl border shadow-xl p-5 max-w-3xl mx-auto flex flex-col h-[500px]">
                <div className="border-b pb-3 mb-4 flex items-center justify-between">
                  <h4 className="font-extrabold text-sm text-blue-950">Live Tutor Support</h4>
                  <span className="bg-emerald-100 text-emerald-800 text-[10px] font-bold px-2 py-0.5 rounded-full">Tutor Ready</span>
                </div>
                <div className="flex-grow overflow-y-auto space-y-3 pr-2 text-xs">
                  {chatMessages.map(msg => (
                    <div key={msg.id} className={`flex flex-col ${msg.role === 'student' ? 'items-end' : 'items-start'}`}>
                      <div className={`p-3 rounded-2xl max-w-[80%] ${msg.role === 'student' ? 'bg-blue-900 text-white' : 'bg-slate-100 text-slate-800 border'}`}>
                        {msg.text}
                      </div>
                    </div>
                  ))}
                </div>
                <form onSubmit={sendChatMessage} className="mt-4 pt-3 border-t flex gap-2">
                  <input type="text" placeholder="Ketik pertanyaanmu..." value={chatInput} onChange={(e) => setChatInput(e.target.value)} className="flex-grow bg-slate-100 border text-xs rounded-2xl px-4 py-2.5" />
                  <button type="submit" className="bg-teal-600 text-white px-5 py-2.5 rounded-2xl font-bold text-xs">Kirim</button>
                </form>
              </div>
            )}
          </div>
        )}

        {/* PILAR 4: MANAJEMEN & ADMINISTRASI */}
        {activeTab === 'manajemen' && (
          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            <div className="bg-white rounded-3xl border shadow-sm p-6 space-y-4">
              <div className="text-center space-y-2">
                <div className="w-20 h-20 rounded-full bg-gradient-to-tr from-blue-900 to-teal-500 text-white text-3xl font-bold flex items-center justify-center mx-auto shadow">
                  {currentUser.avatar}
                </div>
                <h3 className="font-extrabold text-base text-slate-800">{currentUser.fullName}</h3>
                <p className="text-xs text-slate-500">@{currentUser.username}</p>
              </div>

              <div className="pt-4 border-t space-y-2 text-xs">
                <div className="flex justify-between py-1 border-b">
                  <span className="text-slate-500 font-semibold">Email:</span>
                  <span className="font-bold text-slate-800">{currentUser.email}</span>
                </div>
                <div className="flex justify-between py-1 border-b">
                  <span className="text-slate-500 font-semibold">Jenjang:</span>
                  <span className="font-bold text-blue-900">{selectedLevel} ({selectedGrade})</span>
                </div>
                <div className="flex justify-between py-1 border-b">
                  <span className="text-slate-500 font-semibold">Asal Sekolah:</span>
                  <span className="font-bold text-slate-800">{userProfileData.schoolOrigin}</span>
                </div>
              </div>
            </div>

            <div className="lg:col-span-2 bg-white rounded-3xl border shadow-sm p-6 space-y-6">
              <div className="flex items-center justify-between border-b pb-4">
                <div>
                  <h3 className="font-extrabold text-base text-blue-950 flex items-center gap-2"><BarChart2 className="w-5 h-5 text-teal-600" /> Raport Formatif Digital</h3>
                  <p className="text-xs text-slate-500">Capaian Akademik Siswa Kurikulum Nasional.</p>
                </div>
                <button onClick={() => window.print()} className="bg-blue-900 text-white font-bold text-xs px-3.5 py-2 rounded-2xl flex items-center gap-1.5 shadow">
                  <Printer className="w-4 h-4" /> Cetak Raport
                </button>
              </div>

              <div className="overflow-x-auto">
                <table className="w-full text-left text-xs">
                  <thead>
                    <tr className="bg-slate-100 border-b text-slate-700 font-extrabold">
                      <th className="p-3">Mata Pelajaran</th>
                      <th className="p-3">Tingkat</th>
                      <th className="p-3">Nilai Formatif</th>
                      <th className="p-3">Status</th>
                    </tr>
                  </thead>
                  <tbody className="divide-y">
                    {SUBJECTS_LIST.filter(s => s.cat.includes(selectedLevel)).slice(0, 8).map((sub, i) => (
                      <tr key={sub.id}>
                        <td className="p-3 font-bold text-slate-800 flex items-center gap-2"><span>{sub.icon}</span> {sub.name}</td>
                        <td className="p-3 text-slate-500 font-semibold">{selectedLevel}</td>
                        <td className="p-3 font-black text-blue-950">{(85 + (i * 2) % 12).toFixed(1)}</td>
                        <td className="p-3"><span className="bg-emerald-100 text-emerald-800 font-black px-2.5 py-0.5 rounded-full text-[10px]">TUNTAS</span></td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            </div>

          </div>
        )}

      </main>

      {/* DASHBOARD FOOTER */}
      <footer className="bg-blue-950 text-white border-t border-blue-900 py-6 mt-12">
        <div className="max-w-7xl mx-auto px-4 text-center text-xs text-slate-400 space-y-2">
          <p className="font-semibold text-slate-300">Scientists Learning Center — Bimbingan Belajar Kurikulum Nasional SD, SMP, SMA.</p>
        </div>
      </footer>

    </div>
  );
}
