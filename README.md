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

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 to-blue-100 p-4">
      <div className="max-w-2xl mx-auto bg-white/95 rounded-2xl shadow-lg relative overflow-hidden mt-4 p-8">
        {/* SVG Decorations */}
        <svg className="absolute top-12 left-0 w-48 animate-[flyPlane_15s_linear_infinite]" 
             xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 300">
          <g>
            <path d="M180 100 C 190 90, 220 85, 240 90 L 280 100 L 290 95 C 300 90, 320 88, 330 90 L 340 95 L 350 90 L 370 92 L 360 98 L 340 100 L 330 105 C 320 110, 300 112, 290 110 L 280 105 L 240 115 C 220 120, 190 115, 180 105 Z" 
                  fill="#4169E1"/>
            <path d="M290 92 L 300 80 L 320 78 L 310 92" fill="#4169E1"/>
            <path d="M240 108 L 250 120 L 270 122 L 260 108" fill="#4169E1"/>
            <circle cx="200" cy="100" r="8" fill="#333"/>
            <circle cx="320" cy="95" r="6" fill="#333"/>
          </g>
        </svg>

        {/* Rainbow Gradient Border */}
        <div className="absolute top-0 left-0 right-0 h-2 bg-gradient-to-r from-red-400 via-blue-400 to-green-400"></div>

        {/* Main Content */}
        <h1 className="text-2xl md:text-3xl text-center text-red-400 font-semibold mb-2 animate-bounce">
          ลงทะเบียนวันเด็กแห่งชาติ
        </h1>
        <p className="text-lg text-center text-purple-600 font-medium mb-2">
          "ทุกโอกาส คือ การเรียนรู้ พร้อมปรับตัวสู่อนาคตที่เลือกเอง"
        </p>
        <h3 className="text-xl text-center text-blue-400 mb-8 animate-fade-in">
          ณ ศูนย์การฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น ปี 2568
        </h3>

        <form className="space-y-6">
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

          {/* Additional form fields... */}

          <div className="bg-white p-4 rounded-xl shadow-sm">
            <label className="block font-medium text-gray-700 mb-4">
              🎮 กิจกรรมที่สนใจ (เลือกได้หลายกิจกรรม)
            </label>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {activities.map((activity) => (
                <div key={activity.id}
                     className="flex items-center gap-3 p-3 bg-blue-50 rounded-lg hover:bg-blue-100 transition-colors">
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

          <button
            type="submit"
            className="w-full p-3 bg-gradient-to-r from-red-400 to-orange-400 text-white font-semibold rounded-lg hover:translate-y-[-2px] hover:shadow-lg transition-all"
          >
            ✨ ลงทะเบียน
          </button>
        </form>
      </div>

      <footer className="text-center text-gray-600 text-sm mt-8">
        © 2568 งานวันเด็กแห่งชาติ | ศูนย์ฝึกกองทัพอากาศน้ำพอง จังหวัดขอนแก่น
      </footer>
    </div>
  );
};

export default ThaiChildrensDayForm;
