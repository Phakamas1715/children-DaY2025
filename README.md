import React, { useState, useEffect } from 'react';
import { X, Plus } from 'lucide-react';

const ThaiChildrensDayForm = () => {
  // State declarations
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

  // Constants
  const districts = ['เมืองขอนแก่น', 'น้ำพอง', 'กระนวน', 'เขาสวนกวาง', 'อุบลรัตน์'];

  const activities = [
    { id: 'balloon', label: '🎯 ยิงเป้าลูกโป่ง (10 คะแนน)' },
    { id: 'ball', label: '🎳 ปาลูกบอลใส่กระป๋อง (10 คะแนน)' },
    { id: 'plane', label: '✈️ พับเครื่องบินกระดาษ (10 คะแนน)' },
    { id: 'tug', label: '🏃 ชักเย่อ (20 คะแนน)' },
    { id: 'quiz', label: '❓ ตอบคำถาม (20 คะแนน)' },
    { id: 'firstaid', label: '🏥 การปฐมพยาบาลเบื้องต้น (20 คะแนน)' }
  ];

  // Handlers
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

  const toggleActivity = (activityId) => {
    setFormData(prev => ({
      ...prev,
      selectedActivities: prev.selectedActivities.includes(activityId)
        ? prev.selectedActivities.filter(id => id !== activityId)
        : [...prev.selectedActivities, activityId]
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
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
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-100 to-indigo-100 p-6">
      <div className="max-w-2xl mx-auto bg-white/80 backdrop-blur-sm rounded-2xl shadow-xl p-8 relative overflow-hidden">
        {/* Decorative Elements */}
        <div className="absolute top-0 left-0 right-0 h-2 bg-gradient-to-r from-red-400 via-yellow-400 to-blue-400" />
        
        <div className="text-center mb-8 animate__animated animate__bounceIn">
          <h1 className="text-3xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-purple-600 to-pink-600">
            ลงทะเบียนวันเด็กแห่งชาติ
          </h1>
          <h3 className="text-lg text-purple-600 mt-2">
            ณ ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น ปี 2568
          </h3>
        </div>

        <form onSubmit={handleSubmit} className="space-y-6">
          {/* Parent Information */}
          <div className="space-y-4">
            <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
              ข้อมูลผู้ปกครอง
            </h3>
            
            <input
              type="text"
              name="parentName"
              value={formData.parentName}
              onChange={handleInputChange}
              placeholder="ชื่อ-นามสกุล"
              className="w-full px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                        focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
              required
            />

            <input
              type="tel"
              name="parentPhone"
              value={formData.parentPhone}
              onChange={handleInputChange}
              placeholder="เบอร์โทรศัพท์"
              className="w-full px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                        focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
              required
            />
          </div>

          {/* Address Information */}
          <div className="space-y-4">
            <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
              ที่อยู่
            </h3>
            
            <input
              type="text"
              name="address"
              value={formData.address}
              onChange={handleInputChange}
              placeholder="บ้านเลขที่ / หมู่"
              className="w-full px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                        focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
              required
            />

            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              <input
                type="text"
                name="subdistrict"
                value={formData.subdistrict}
                onChange={handleInputChange}
                placeholder="ตำบล"
                className="w-full px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                          focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
                required
              />

              <select
                name="district"
                value={formData.district}
                onChange={handleInputChange}
                className="w-full px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                          focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
                required
              >
                <option value="">เลือกอำเภอ</option>
                {districts.map(district => (
                  <option key={district} value={district}>{district}</option>
                ))}
              </select>
            </div>
          </div>

          {/* Children Section */}
          <div className="space-y-4">
            <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
              ข้อมูลเด็ก
            </h3>

            {formData.children.map(child => (
              <div key={child.id} className="flex items-center gap-4 group">
                <input
                  type="text"
                  value={child.name}
                  onChange={(e) => updateChild(child.id, 'name', e.target.value)}
                  placeholder="ชื่อ-นามสกุล"
                  className="flex-1 px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                            focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
                  required
                />
                <input
                  type="number"
                  value={child.age}
                  onChange={(e) => updateChild(child.id, 'age', e.target.value)}
                  placeholder="อายุ"
                  className="w-24 px-4 py-2 rounded-lg border border-purple-200 focus:border-purple-400 
                            focus:ring-2 focus:ring-purple-200 outline-none transition-all duration-300"
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

          {/* Activities Section */}
          <div className="space-y-4">
            <h3 className="text-xl font-semibold text-purple-700 flex items-center gap-2">
              กิจกรรมที่สนใจ
            </h3>

            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {activities.map(activity => (
                <label
                  key={activity.id}
                  className="flex items-center gap-3 p-3 rounded-lg border border-purple-200
                           hover:border-purple-400 hover:bg-purple-50 transition-all duration-300 cursor-pointer"
                >
                  <input
                    type="checkbox"
                    checked={formData.selectedActivities.includes(activity.id)}
                    onChange={() => toggleActivity(activity.id)}
                    className="w-5 h-5 rounded text-purple-500 focus:ring-purple-400"
                  />
                  <span>{activity.label}</span>
                </label>
              ))}
            </div>
          </div>

          {/* Rewards Information */}
          <div className="bg-gradient-to-r from-pink-50 to-purple-50 p-6 rounded-lg border border-purple-200">
            <h4 className="text-xl font-semibold text-purple-700 mb-4 text-center">
              🎁 เงื่อนไขการแลกรางวัล
            </h4>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div className="p-4 bg-white rounded-lg shadow-sm text-center">
                <div className="text-xl font-bold text-purple-600">30-50 คะแนน</div>
                <div className="text-gray-600">แลกรับรางวัล</div>
              </div>
              <div className="p-4 bg-white rounded-lg shadow-sm text-center">
                <div className="text-xl font-bold text-purple-600">100 คะแนน</div>
                <div className="text-gray-600">รางวัลพิเศษ</div>
              </div>
            </div>
            <p className="text-sm text-gray-500 text-center mt-4">
              * คะแนนจะแสดงหลังจากสแกน QR Code ในแต่ละฐาน
            </p>
          </div>

          {/* Submit Button */}
          <button
            type="submit"
            className="w-full py-3 px-6 bg-gradient-to-r from-purple-600 to-pink-600 text-white font-medium
                     rounded-lg shadow-lg hover:shadow-xl transform hover:-translate-y-0.5 transition-all
