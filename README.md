import React, { useState } from 'react';
import { X, Plus, MapPin, Home, Phone, Users, Globe, Send } from 'lucide-react';

const ThaiChildrensDayForm = () => {
  const [formData, setFormData] = useState({
    parentName: '',
    parentPhone: '',
    address: '',
    subdistrict: '',
    district: '',
    children: [],
    selectedActivities: []
  });

  const [showResult, setShowResult] = useState(false);
  const [registrationId, setRegistrationId] = useState('');

  const districts = ['เมืองขอนแก่น', 'น้ำพอง', 'กระนวน', 'เขาสวนกวาง', 'อุบลรัตน์'];

  const activities = [
    { id: 'balloon', label: '🎯 ยิงเป้าลูกโป่ง (10 คะแนน)' },
    { id: 'ball', label: '🎳 ปาลูกบอลใส่กระป๋อง (10 คะแนน)' },
    { id: 'plane', label: '✈️ พับเครื่องบินกระดาษ (10 คะแนน)' },
    { id: 'tug', label: '🏃 ชักเย่อ (20 คะแนน)' },
    { id: 'quiz', label: '❓ ตอบคำถาม (20 คะแนน)' },
    { id: 'firstaid', label: '🏥 การปฐมพยาบาลเบื้องต้น (20 คะแนน)' }
  ];

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const addChild = () => {
    setFormData(prev => ({
      ...prev,
      children: [...prev.children, { id: Date.now(), name: '', age: '' }]
    }));
  };

  const removeChild = (childId) => {
    setFormData(prev => ({
      ...prev,
      children: prev.children.filter(child => child.id !== childId)
    }));
  };

  const updateChild = (childId, field, value) => {
    setFormData(prev => ({
      ...prev,
      children: prev.children.map(child =>
        child.id === childId ? { ...child, [field]: value } : child
      )
    }));
  };

  const handleActivityToggle = (activityId) => {
    setFormData(prev => ({
      ...prev,
      selectedActivities: prev.selectedActivities.includes(activityId)
        ? prev.selectedActivities.filter(id => id !== activityId)
        : [...prev.selectedActivities, activityId]
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    
    // สร้างรหัสลงทะเบียน 4 หลัก
    const uid = String(Math.floor(Math.random() * 9000) + 1000);
    
    try {
      const response = await fetch('https://script.google.com/macros/s/AKfycbzUB3g5P-8HWHEiU-xwn5Y5gsbScC78_sBrC6tnItdcGSoDGvztdGpaqt_39CLh1XNT/exec', {
        method: 'POST',
        body: JSON.stringify({ ...formData, uid })
      });

      if (!response.ok) throw new Error('การส่งข้อมูลล้มเหลว');

      setRegistrationId(uid);
      setShowResult(true);
    } catch (error) {
      alert('เกิดข้อผิดพลาด: ' + error.message);
    }
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-100 to-indigo-100 py-12 px-4 sm:px-6 lg:px-8">
      <div className="max-w-4xl mx-auto">
        {/* Flying Plane Animation */}
        <div className="absolute top-10 left-0 w-full overflow-hidden pointer-events-none">
          <div className="animate-fly">
            <span className="text-4xl">✈️</span>
          </div>
        </div>

        <div className="bg-white/80 backdrop-blur-sm rounded-2xl shadow-xl p-8 space-y-8">
          <div className="text-center space-y-4">
            <h1 className="text-4xl font-bold bg-gradient-to-r from-purple-600 to-pink-600 bg-clip-text text-transparent animate-bounce">
              ลงทะเบียนวันเด็กแห่งชาติ
            </h1>
            <h2 className="text-xl text-gray-600">
              ณ ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น ปี 2568
            </h2>
          </div>

          <form onSubmit={handleSubmit} className="space-y-6">
            {/* Parent Information */}
            <div className="space-y-4">
              <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
                <Users className="w-5 h-5" />
                ข้อมูลผู้ปกครอง
              </h3>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <input
                  type="text"
                  name="parentName"
                  value={formData.parentName}
                  onChange={handleInputChange}
                  placeholder="ชื่อ-นามสกุล"
                  className="input-field"
                  required
                />
                <input
                  type="tel"
                  name="parentPhone"
                  value={formData.parentPhone}
                  onChange={handleInputChange}
                  placeholder="เบอร์โทรศัพท์"
                  className="input-field"
                  required
                />
              </div>
            </div>

            {/* Address Section */}
            <div className="space-y-4">
              <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
                <MapPin className="w-5 h-5" />
                ที่อยู่
              </h3>
              
              <div className="space-y-4">
                <input
                  type="text"
                  name="address"
                  value={formData.address}
                  onChange={handleInputChange}
                  placeholder="บ้านเลขที่ / หมู่บ้าน"
                  className="input-field"
                  required
                />
                
                <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <input
                    type="text"
                    name="subdistrict"
                    value={formData.subdistrict}
                    onChange={handleInputChange}
                    placeholder="ตำบล"
                    className="input-field"
                    required
                  />
                  <select
                    name="district"
                    value={formData.district}
                    onChange={handleInputChange}
                    className="input-field"
                    required
                  >
                    <option value="">เลือกอำเภอ</option>
                    {districts.map(district => (
                      <option key={district} value={district}>
                        {district}
                      </option>
                    ))}
                  </select>
                </div>
              </div>
            </div>

            {/* Children Section */}
            <div className="space-y-4">
              <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
                <Users className="w-5 h-5" />
                ข้อมูลเด็ก
              </h3>
              
              <div className="space-y-4">
                {formData.children.map((child) => (
                  <div key={child.id} className="flex items-center gap-4 group">
                    <input
                      type="text"
                      value={child.name}
                      onChange={(e) => updateChild(child.id, 'name', e.target.value)}
                      placeholder="ชื่อ-นามสกุล"
                      className="input-field flex-1"
                      required
                    />
                    <input
                      type="number"
                      value={child.age}
                      onChange={(e) => updateChild(child.id, 'age', e.target.value)}
                      placeholder="อายุ"
                      className="input-field w-24"
                      min="1"
                      max="15"
                      required
                    />
                    <button
                      type="button"
                      onClick={() => removeChild(child.id)}
                      className="p-2 text-red-500 hover:bg-red-100 rounded-full transition-colors duration-300"
                    >
                      <X className="w-5 h-5" />
                    </button>
                  </div>
                ))}
                
                <button
                  type="button"
                  onClick={addChild}
                  className="w-full py-2 px-4 border-2 border-dashed border-purple-300 rounded-lg
                           hover:border-purple-400 hover:bg-purple-50 transition-all duration-300
                           text-purple-600 font-medium flex items-center justify-center gap-2"
                >
                  <Plus className="w-5 h-5" />
                  เพิ่มข้อมูลเด็ก
                </button>
              </div>
            </div>

            {/* Activities Section */}
            <div className="space-y-4">
              <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
                <Globe className="w-5 h-5" />
                กิจกรรมที่สนใจ
              </h3>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                {activities.map((activity) => (
                  <label
                    key={activity.id}
                    className="flex items-center gap-3 p-3 rounded-lg border border-purple-200
                             hover:border-purple-400 hover:bg-purple-50 transition-all duration-300 cursor-pointer"
                  >
                    <input
                      type="checkbox"
                      checked={formData.selectedActivities.includes(activity.id)}
                      onChange={() => handleActivityToggle(activity.id)}
                      className="w-5 h-5 rounded text-purple-500 focus:ring-purple-400"
                    />
                    <span>{activity.label}</span>
                  </label>
                ))}
              </div>
            </div>

            {/* Rewards Info */}
            <div className="bg-gradient-to-r from-pink-50 to-purple-50 rounded-xl p-6 border-2 border-dashed border-purple-200">
              <h4 className="text-xl font-semibold text-center text-purple-700 mb-4">
                🎁 เงื่อนไขการแลกรางวัล
              </h4>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div className="bg-white rounded-lg p-4 text-center shadow-md hover:shadow-lg transition-shadow">
                  <div className="text-2xl font-bold text-purple-600">30-50 คะแนน</div>
                  <div className="text-gray-600">แลกรับรางวัล</div>
                </div>
                <div className="bg-white rounded-lg p-4 text-center shadow-md hover:shadow-lg transition-shadow">
                  <div className="text-2xl font-bold text-purple-600">100 คะแนน</div>
                  <div className="text-gray-600">รางวัลพิเศษ</div>
                </div>
              </div>
              <p className="text-center text-sm text-gray-500 mt-4">
                * คะแนนจะแสดงหลังจากสแกน QR Code ในแต่ละฐาน
              </p>
            </div>

            {/* Submit Button */}
            <button
              type="submit"
              className="w-full py-3 px-6 bg-gradient-to-r from-purple-600 to-pink-600 text-white font-medium
                       rounded-lg shadow-lg hover:shadow-xl transform hover:-translate-y-0.5 transition-all
                       duration-300 flex items-center justify-center gap-2"
            >
              <Send className="w-5 h-5" />
              ลงทะเบียน
            </button>
          </form>

          {/* Result Modal */}
          {showResult && (
            <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4">
              <div className="bg-white rounded-2xl p-8 max-w-md w-full animate-scale-up">
                <h3 className="text-2xl font-bold text-center text
