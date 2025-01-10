import React, { useState } from 'react';
import { X, Plus, MapPin, Home, Phone, Users, Globe } from 'lucide-react';

const ThaiChildrensDayForm = () => {
  const [parentName, setParentName] = useState('');
  const [parentPhone, setParentPhone] = useState('');
  const [address, setAddress] = useState('');
  const [subdistrict, setSubdistrict] = useState('');
  const [district, setDistrict] = useState('');
  const [children, setChildren] = useState([]);
  const [selectedActivities, setSelectedActivities] = useState([]);

  const districts = [
    'เมืองขอนแก่น',
    'น้ำพอง',
    'กระนวน',
    'เขาสวนกวาง',
    'อุบลรัตน์'
  ];

  const activities = [
    { id: 'balloon', label: '🎯 ยิงเป้าลูกโป่ง (10 คะแนน)' },
    { id: 'ball', label: '🎳 ปาลูกบอลใส่กระป๋อง (10 คะแนน)' },
    { id: 'plane', label: '✈️ พับเครื่องบินกระดาษ (10 คะแนน)' },
    { id: 'tug', label: '🏃 ชักเย่อ (20 คะแนน)' },
    { id: 'quiz', label: '❓ ตอบคำถาม (20 คะแนน)' },
    { id: 'firstaid', label: '🏥 การปฐมพยาบาลเบื้องต้น (20 คะแนน)' }
  ];

  const addChild = () => {
    setChildren([...children, {
      id: Date.now(),
      name: '',
      age: ''
    }]);
  };

  const removeChild = (childId) => {
    setChildren(children.filter(child => child.id !== childId));
  };

  const updateChild = (childId, field, value) => {
    setChildren(children.map(child =>
      child.id === childId ? { ...child, [field]: value } : child
    ));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // Handle form submission
    console.log({
      parentName,
      parentPhone,
      address,
      subdistrict,
      district,
      children,
      selectedActivities
    });
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 to-blue-100 p-4">
      <div className="max-w-2xl mx-auto bg-white/95 rounded-2xl shadow-lg relative overflow-hidden mt-4 p-8">
        {/* Rainbow Gradient Border */}
        <div className="absolute top-0 left-0 right-0 h-2 bg-gradient-to-r from-red-400 via-blue-400 to-green-400" />

        {/* Form Header */}
        <h1 className="text-3xl text-center text-red-400 font-semibold mb-2 animate-bounce">
          ลงทะเบียนวันเด็กแห่งชาติ ประจำปี พ.ศ.2568
        </h1>
        <p className="text-lg text-center text-purple-600 font-medium mb-2">
          "ทุกโอกาส คือ การเรียนรู้ พร้อมปรับตัวสู่อนาคตที่เลือกเอง"
        </p>
        <h3 className="text-xl text-center text-blue-400 mb-8">
          ณ ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น ปี 2568
        </h3>

        {/* Registration Form */}
        <form onSubmit={handleSubmit} className="space-y-6">
          {/* Parent Information */}
          <div className="bg-white p-4 rounded-xl shadow-sm hover:translate-y-[-2px] transition-transform">
            <label className="flex items-center gap-2 mb-2 font-medium text-gray-700">
              <Users className="w-5 h-5" />
              ชื่อ-นามสกุลผู้ปกครอง
            </label>
            <input
              type="text"
              value={parentName}
              onChange={(e) => setParentName(e.target.value)}
              className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50 focus:border-blue-400 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="กรุณากรอกชื่อ-นามสกุล"
              required
            />
          </div>

          {/* Phone */}
          <div className="bg-white p-4 rounded-xl shadow-sm hover:translate-y-[-2px] transition-transform">
            <label className="flex items-center gap-2 mb-2 font-medium text-gray-700">
              <Phone className="w-5 h-5" />
              เบอร์โทรศัพท์
            </label>
            <input
              type="tel"
              value={parentPhone}
              onChange={(e) => setParentPhone(e.target.value)}
              className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50 focus:border-blue-400 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="กรุณากรอกเบอร์โทรศัพท์"
              required
            />
          </div>

          {/* Address */}
          <div className="bg-white p-4 rounded-xl shadow-sm hover:translate-y-[-2px] transition-transform">
            <label className="flex items-center gap-2 mb-2 font-medium text-gray-700">
              <Home className="w-5 h-5" />
              ที่อยู่
            </label>
            <input
              type="text"
              value={address}
              onChange={(e) => setAddress(e.target.value)}
              className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50 focus:border-blue-400 focus:ring-2 focus:ring-blue-200 transition-all"
              placeholder="บ้านเลขที่ / หมู่"
              required
            />
          </div>

          {/* District Selection */}
          <div className="bg-white p-4 rounded-xl shadow-sm hover:translate-y-[-2px] transition-transform">
            <label className="flex items-center gap-2 mb-2 font-medium text-gray-700">
              <Globe className="w-5 h-5" />
              อำเภอ
            </label>
            <select
              value={district}
              onChange={(e) => setDistrict(e.target.value)}
              className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50 focus:border-blue-400 focus:ring-2 focus:ring-blue-200 transition-all"
              required
            >
              <option value="">เลือกอำเภอ</option>
              {districts.map((d) => (
                <option key={d} value={d}>{d}</option>
              ))}
            </select>
          </div>

          {/* Children Information */}
          {children.map((child, index) => (
            <div key={child.id} className="bg-white p-4 rounded-xl shadow-sm hover:translate-y-[-2px] transition-transform relative">
              <button
                type="button"
                onClick={() => removeChild(child.id)}
                className="absolute top-2 right-2 text-red-400 hover:bg-red-50 p-1 rounded-full"
              >
                <X className="w-5 h-5" />
              </button>
              <div className="space-y-4">
                <div>
                  <label className="block mb-2 font-medium text-gray-700">
                    👶 ชื่อเด็กคนที่ {index + 1}
                  </label>
                  <input
                    type="text"
                    value={child.name}
                    onChange={(e) => updateChild(child.id, 'name', e.target.value)}
                    className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50"
                    placeholder="กรุณากรอกชื่อเด็ก"
                    required
                  />
                </div>
                <div>
                  <label className="block mb-2 font-medium text-gray-700">
                    🎂 อายุ
                  </label>
                  <input
                    type="number"
                    min="1"
                    max="15"
                    value={child.age}
                    onChange={(e) => updateChild(child.id, 'age', e.target.value)}
                    className="w-full p-3 border-2 border-indigo-100 rounded-lg bg-blue-50/50"
                    placeholder="กรุณากรอกอายุ"
                    required
                  />
                </div>
              </div>
            </div>
          ))}

          {/* Add Child Button */}
          <button
            type="button"
            onClick={addChild}
            className="w-full p-3 bg-gradient-to-r from-blue-400 to-cyan-400 text-white font-semibold rounded-lg hover:translate-y-[-2px] hover:shadow-lg transition-all flex items-center justify-center gap-2"
          >
            <Plus className="w-5 h-5" />
            เพิ่มข้อมูลเด็ก
          </button>

          {/* Activities Section */}
          <div className="bg-white p-4 rounded-xl shadow-sm">
            <label className="block font-medium text-gray-700 mb-4">
              🎮 กิจกรรมที่สนใจ (เลือกได้หลายกิจกรรม)
            </label>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {activities.map((activity) => (
                <div
                  key={activity.id}
                  className="flex items-center gap-3 p-3 bg-blue-50 rounded-lg hover:bg-blue-100 transition-colors"
                >
                  <input
                    type="checkbox"
                    id={activity.id}
                    className="w-5 h-5"
                    checked={selectedActivities.includes(activity.id)}
                    onChange={(e) => {
                      if (e.target.checked) {
                        setSelectedActivities([...selectedActivities, activity.id]);
                      } else {
                        setSelectedActivities(selectedActivities.filter(id => id !== activity.id));
                      }
                    }}
                  />
                  <label htmlFor={activity.id} className="cursor-pointer">
                    {activity.label}
                  </label>
                </div>
              ))}
            </div>
          </div>

          {/* Rewards Information */}
          <div className="bg-gradient-to-r from-pink-50 to-red-50 p-6 rounded-xl border-2 border-dashed border-pink-200">
            <h4 className="text-xl text-red-400 text-center font-semibold mb-4">
              🎁 เงื่อนไขการแลกรางวัล
            </h4>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div className="bg-white p-4 rounded-lg shadow-sm text-center hover:translate-y-[-3px] transition-transform">
                <div className="text-lg font-bold text-blue-600 mb-2">30-50 คะแนน</div>
                <div className="text-gray-600">แลกรับรางวัล</div>
              </div>
              <div className="bg-white p-4 rounded-lg shadow-sm text-center hover:translate-y-[-3px] transition-transform">
                <div className="text-lg font-bold text-blue-600 mb-2">100 คะแนน</div>
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
            className="w-full p-3 bg-gradient-to-r from-red-400 to-orange-400 text-white font-semibold rounded-lg hover:translate-y-[-2px] hover:shadow-lg transition-all"
          >
            ✨ ลงทะเบียน
          </button>
        </form>
      </div>

      <footer className="text-center text-gray-600 text-sm mt-8">
        © 2568 งานวันเด็กแห่งชาติ | ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น
      </footer>
    </div>
  );
};

export default ThaiChildrensDayForm;
