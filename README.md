import { useState } from "react";

const artisans = [
  { id: 1, name: "محمد الرخامي", job: "رخام", city: "الدار البيضاء", experience: 12, phone: "0600000000", whatsapp: "0600000000" },
  { id: 2, name: "سعيد البنّاء", job: "بناء", city: "فاس", experience: 8, phone: "0600000001", whatsapp: "0600000001" },
];

export default function Home() {
  // بحث
  const [city, setCity] = useState("");
  const [job, setJob] = useState("");
  const [results, setResults] = useState([]);
  // تسجيل
  const [name, setName] = useState("");
  const [regJob, setRegJob] = useState("");
  const [regCity, setRegCity] = useState("");
  const [experience, setExperience] = useState("");
  const [phone, setPhone] = useState("");
  const [whatsapp, setWhatsapp] = useState("");
  // تفاصيل
  const [selectedArtisan, setSelectedArtisan] = useState(null);

  function handleSearch() {
    setResults(
      artisans.filter(a =>
        (!city || a.city === city) && (!job || a.job === job)
      )
    );
    setSelectedArtisan(null);
  }

  function handleRegister(e) {
    e.preventDefault();
    alert("تم تسجيلك بنجاح! (تجريبي)");
    // يمكن هنا إضافة الحرفي إلى مصفوفة الحرفيين (artisans)
  }

  return (
    <div dir="rtl" style={{padding: "2rem"}}>
      <h1>دليل الحرفيين المغاربة</h1>
      {/* البحث */}
      <h2>البحث عن الحرفيين</h2>
      <input placeholder="المدينة" value={city} onChange={e => setCity(e.target.value)} />
      <input placeholder="نوع الحرفة" value={job} onChange={e => setJob(e.target.value)} />
      <button onClick={handleSearch}>بحث</button>
      <ul>
        {results.map(a => (
          <li key={a.id}>
            <button onClick={() => setSelectedArtisan(a)}>
              {a.name} - {a.job} - {a.city}
            </button>
          </li>
        ))}
      </ul>
      {/* تفاصيل الحرفي */}
      {selectedArtisan && (
        <div style={{border:"1px solid #ccc", margin:"1rem", padding:"1rem"}}>
          <h3>بيانات الحرفي</h3>
          <p>الإسم: {selectedArtisan.name}</p>
          <p>نوع الحرفة: {selectedArtisan.job}</p>
          <p>المدينة: {selectedArtisan.city}</p>
          <p>سنوات الخبرة: {selectedArtisan.experience}</p>
          <p>رقم الهاتف: <a href={`tel:${selectedArtisan.phone}`}>{selectedArtisan.phone}</a></p>
          <p>واتساب: <a href={`https://wa.me/${selectedArtisan.whatsapp}`} target="_blank" rel="noopener noreferrer">تواصل واتساب</a></p>
        </div>
      )}
      {/* تسجيل الحرفي */}
      <h2>تسجيل الحرفي الجديد</h2>
      <form onSubmit={handleRegister}>
        <input placeholder="الإسم الكامل" value={name} onChange={e => setName(e.target.value)} required /><br/>
        <input placeholder="نوع الحرفة" value={regJob} onChange={e => setRegJob(e.target.value)} required /><br/>
        <input placeholder="المدينة" value={regCity} onChange={e => setRegCity(e.target.value)} required /><br/>
        <input placeholder="سنوات الخبرة" value={experience} onChange={e => setExperience(e.target.value)} required /><br/>
        <input placeholder="رقم الهاتف" value={phone} onChange={e => setPhone(e.target.value)} required /><br/>
        <input placeholder="رقم واتساب" value={whatsapp} onChange={e => setWhatsapp(e.target.value)} required /><br/>
        <button type="submit">تسجيل</button>
      </form>
    </div>
  );
}
