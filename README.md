# DB-munch1ax.github.io
import React, { useState } from 'react';
import { Users, Building, PieChart, ArrowRight, Wallet } from 'lucide-react';

const BudgetSheet = () => {
  const [activeOrg, setActiveOrg] = useState('clubAlliance'); // clubAlliance (총동연) or council (총대의원회)

  // 데이터 1: 총동아리연합회 (PDF 내용 기반)
  const clubAllianceBudget = [
    {
      category: "동아리 박람회",
      items: [
        { name: "행사 진행 식대", detail: "8명 * 9,000원", cost: 72000, note: "행사 진행 식대" },
        { name: "진행 물품 대여비", detail: "1식", cost: 500000, note: "진행 물품 대여" },
        { name: "예비비", detail: "1식", cost: 98000, note: "예비비" },
      ],
      subtotal: 670000
    },
    {
      category: "1학기 동아리의 밤",
      items: [
        { name: "음향 팀", detail: "(주)탑플랜엔터테인먼트", cost: 6050000, note: "음향업체 및 영상 중계" },
        { name: "공연 MC", detail: "이노베이 주식회사", cost: 300000, note: "" },
        { name: "기타 물품", detail: "미정", cost: 687000, note: "사진 이벤트 및 행사진행용품" },
        { name: "쿠폰", detail: "음주다방, 세이커피", cost: 46000, note: "" },
        { name: "자선 사업 수익", detail: "수익 차감", cost: -200000, note: "사진 촬영 행사 사업 (예상 수익)" },
      ],
      subtotal: 6883000
    },
    {
      category: "2학기 동아리의 밤",
      items: [
        { name: "음향 팀", detail: "(주)탑플랜엔터테인먼트", cost: 4050000, note: "음향업체 및 특수효과" },
        { name: "공연 MC", detail: "(주)탑플랜엔터테인먼트", cost: 500000, note: "" },
        { name: "기타 물품", detail: "미정", cost: 400000, note: "행사 진행 용품" },
        { name: "쿠폰", detail: "음주다방, 세이커피", cost: 53000, note: "" },
      ],
      subtotal: 5003000
    },
    {
      category: "동아리 성과발표제",
      items: [
        { name: "시상금 (1등)", detail: "1팀", cost: 800000, note: "" },
        { name: "시상금 (2등)", detail: "1팀", cost: 500000, note: "" },
        { name: "시상금 (3등)", detail: "1팀", cost: 300000, note: "" },
        { name: "장려상", detail: "1팀", cost: 100000, note: "" },
        { name: "간식 및 음료", detail: "", cost: 200000, note: "" },
      ],
      subtotal: 1900000
    }
  ];

  // 데이터 2: 총대의원회 (채팅 입력 내용 기반)
  const councilBudget = [
    {
      category: "감사용",
      desc: "감사, 청문회, 대의원총회 등 운영 및 검증 비용",
      items: [
        { name: "상반기 1차 감사 식대", cost: 350000 },
        { name: "청문회 부식비", cost: 50000 },
        { name: "상반기 2차 감사 식대", cost: 350000 },
        { name: "대의원총회 부식비", cost: 150000 },
        { name: "하반기 1차 감사 식대", cost: 420000 },
      ],
      subtotal: 1320000
    },
    {
      category: "선거용",
      desc: "선관위 운영 및 선거 기간 식대",
      items: [
        { name: "선관위 부식비", cost: 40000 },
        { name: "청문회 및 선거 부식비", cost: 200000 },
        { name: "총학 선거 식대", cost: 600000 },
        { name: "재선거 식대", cost: 500000 },
      ],
      subtotal: 1340000
    },
    {
      category: "사무 및 운영용",
      desc: "일반 사업 운영 비용 (과잠, 행사, 회의비 등)",
      items: [
        { name: "대의원 과잠 및 명찰 구입", cost: 750000 },
        { name: "전년도 스카", cost: 420000 },
        { name: "학회장 회의 부식비", cost: 150000 },
        { name: "농활 진행요원 단체복 및 국원 과잠", cost: 800000 },
        { name: "스피드 카피 (복사/인쇄)", cost: 400000 },
        { name: "대동제 부스 운영 및 경품", cost: 1600000 },
        { name: "주간부스 식대", cost: 150000 },
        { name: "간담회", cost: 300000 },
        { name: "유류비 총계", cost: 250000 },
      ],
      subtotal: 4820000
    }
  ];

  // 총계 계산
  const allianceTotal = clubAllianceBudget.reduce((acc, curr) => acc + curr.subtotal, 0);
  const councilTotal = councilBudget.reduce((acc, curr) => acc + curr.subtotal, 0);
  const grandTotal = allianceTotal + councilTotal;

  const formatCurrency = (amount) => {
    return new Intl.NumberFormat('ko-KR').format(amount);
  };

  return (
    <div className="max-w-5xl mx-auto p-6 bg-gray-50 min-h-screen font-sans">
      <div className="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden">
        
        {/* 메인 헤더 */}
        <div className="p-8 border-b border-gray-200 bg-slate-900 text-white">
          <div className="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
            <div>
              <div className="flex items-center gap-2 mb-2">
                <Wallet className="text-yellow-400" size={24} />
                <h1 className="text-2xl font-bold">2025학년도 학생자치기구 통합 예산안</h1>
              </div>
              <p className="text-slate-300 text-sm pl-8">총동아리연합회 및 총대의원회 예산 내역서</p>
            </div>
            <div className="bg-slate-800 px-6 py-3 rounded-lg border border-slate-700 text-right min-w-[200px]">
              <p className="text-xs text-slate-400 mb-1">전체 통합 예산</p>
              <p className="text-3xl font-bold text-yellow-400">{formatCurrency(grandTotal)}원</p>
            </div>
          </div>
        </div>

        {/* 조직 선택 탭 (대분류) */}
        <div className="grid grid-cols-2 border-b border-gray-200 bg-gray-100 p-2 gap-2">
          <button
            onClick={() => setActiveOrg('clubAlliance')}
            className={`py-4 px-6 rounded-lg text-center font-medium transition-all duration-200 flex flex-col items-center justify-center gap-2 ${
              activeOrg === 'clubAlliance'
                ? 'bg-white text-indigo-900 shadow-sm ring-1 ring-black/5'
                : 'text-gray-500 hover:bg-gray-200 hover:text-gray-700'
            }`}
          >
            <div className="flex items-center gap-2">
              <Users size={20} className={activeOrg === 'clubAlliance' ? 'text-indigo-600' : ''} />
              <span className="text-lg">총동아리연합회</span>
            </div>
            <span className={`text-sm px-2 py-0.5 rounded-full ${
               activeOrg === 'clubAlliance' ? 'bg-indigo-100 text-indigo-800' : 'bg-gray-200 text-gray-500'
            }`}>
              행사 예산 {formatCurrency(allianceTotal)}원
            </span>
          </button>
          
          <button
            onClick={() => setActiveOrg('council')}
            className={`py-4 px-6 rounded-lg text-center font-medium transition-all duration-200 flex flex-col items-center justify-center gap-2 ${
              activeOrg === 'council'
                ? 'bg-white text-emerald-900 shadow-sm ring-1 ring-black/5'
                : 'text-gray-500 hover:bg-gray-200 hover:text-gray-700'
            }`}
          >
            <div className="flex items-center gap-2">
              <Building size={20} className={activeOrg === 'council' ? 'text-emerald-600' : ''} />
              <span className="text-lg">총대의원회</span>
            </div>
            <span className={`text-sm px-2 py-0.5 rounded-full ${
               activeOrg === 'council' ? 'bg-emerald-100 text-emerald-800' : 'bg-gray-200 text-gray-500'
            }`}>
              운영 예산 {formatCurrency(councilTotal)}원
            </span>
          </button>
        </div>

        {/* 상세 내역 컨텐츠 */}
        <div className="p-8 bg-white min-h-[500px]">
          {activeOrg === 'clubAlliance' ? (
            <div className="space-y-8 animate-fade-in">
              <div className="flex items-center gap-3 pb-4 border-b border-indigo-100">
                <div className="w-10 h-10 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600">
                  <Users size={20} />
                </div>
                <div>
                  <h2 className="text-xl font-bold text-gray-800">총동아리연합회 행사 비용</h2>
                  <p className="text-sm text-gray-500">동아리 박람회 및 축제 등 주요 행사 예산</p>
                </div>
              </div>

              {clubAllianceBudget.map((event, index) => (
                <div key={index} className="border border-gray-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
                  <div className="bg-gradient-to-r from-indigo-50 to-white px-5 py-3 border-b border-indigo-100 flex justify-between items-center">
                    <h3 className="font-bold text-indigo-900 text-lg flex items-center gap-2">
                      <span className="w-1.5 h-6 bg-indigo-500 rounded-full block"></span>
                      {event.category}
                    </h3>
                    <span className="font-bold text-indigo-700 bg-white px-3 py-1 rounded-full border border-indigo-100 shadow-sm">
                      {formatCurrency(event.subtotal)}원
                    </span>
                  </div>
                  <div className="p-0">
                    <table className="w-full text-sm text-left">
                      <thead className="bg-gray-50 text-gray-500 border-b border-gray-100">
                        <tr>
                          <th className="px-5 py-3 font-medium w-[30%]">항목</th>
                          <th className="px-5 py-3 font-medium w-[30%]">세부내용/업체</th>
                          <th className="px-5 py-3 font-medium text-right text-xs uppercase tracking-wider">비고</th>
                          <th className="px-5 py-3 font-medium text-right">금액</th>
                        </tr>
                      </thead>
                      <tbody className="divide-y divide-gray-50">
                        {event.items.map((item, i) => (
                          <tr key={i} className="hover:bg-indigo-50/30 transition-colors">
                            <td className="px-5 py-3 font-medium text-gray-800">{item.name}</td>
                            <td className="px-5 py-3 text-gray-600">{item.detail}</td>
                            <td className="px-5 py-3 text-right text-gray-400 text-xs">{item.note}</td>
                            <td className={`px-5 py-3 text-right font-medium ${item.cost < 0 ? 'text-red-500' : 'text-gray-900'}`}>
                              {formatCurrency(item.cost)}
                            </td>
                          </tr>
                        ))}
                      </tbody>
                    </table>
                  </div>
                </div>
              ))}
            </div>
          ) : (
            <div className="space-y-8 animate-fade-in">
              <div className="flex items-center gap-3 pb-4 border-b border-emerald-100">
                <div className="w-10 h-10 rounded-full bg-emerald-100 flex items-center justify-center text-emerald-600">
                  <Building size={20} />
                </div>
                <div>
                  <h2 className="text-xl font-bold text-gray-800">총대의원회 운영 비용</h2>
                  <p className="text-sm text-gray-500">감사, 선거 관리 및 사무 운영 예산</p>
                </div>
              </div>

              <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
                 {councilBudget.map((cat, idx) => (
                   <div key={idx} className="bg-white p-5 rounded-xl border border-gray-200 shadow-sm hover:border-emerald-200 hover:shadow-md transition-all">
                      <h4 className="font-bold text-gray-700 text-lg mb-2">{cat.category}</h4>
                      <p className="text-xs text-gray-500 mb-4 h-8">{cat.desc}</p>
                      <div className="text-right border-t border-gray-100 pt-3">
                        <span className="text-2xl font-bold text-emerald-600">{formatCurrency(cat.subtotal)}</span>
                        <span className="text-sm text-gray-400 ml-1">원</span>
                      </div>
                   </div>
                 ))}
              </div>

              {councilBudget.map((cat, index) => (
                <div key={index} className="border border-gray-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
                  <div className="bg-gradient-to-r from-emerald-50 to-white px-5 py-3 border-b border-emerald-100 flex justify-between items-center">
                    <h3 className="font-bold text-emerald-900 text-lg flex items-center gap-2">
                       <span className={`w-1.5 h-6 rounded-full block ${
                         index === 0 ? 'bg-blue-500' : index === 1 ? 'bg-orange-500' : 'bg-emerald-500'
                       }`}></span>
                      {cat.category}
                    </h3>
                    <span className="font-bold text-emerald-700 bg-white px-3 py-1 rounded-full border border-emerald-100 shadow-sm">
                      {formatCurrency(cat.subtotal)}원
                    </span>
                  </div>
                  <table className="w-full text-sm text-left">
                    <thead className="bg-gray-50 text-gray-500 border-b border-gray-100">
                      <tr>
                        <th className="px-5 py-3 font-medium text-gray-600">세부 항목 명</th>
                        <th className="px-5 py-3 font-medium text-right text-gray-600">지출 금액</th>
                      </tr>
                    </thead>
                    <tbody className="divide-y divide-gray-50">
                      {cat.items.map((item, i) => (
                        <tr key={i} className="hover:bg-emerald-50/30 transition-colors">
                          <td className="px-5 py-3 font-medium text-gray-800">{item.name}</td>
                          <td className="px-5 py-3 text-right font-bold text-gray-900">{formatCurrency(item.cost)}</td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              ))}
            </div>
          )}
        </div>
        
        {/* 통합 요약 푸터 */}
        <div className="bg-gray-900 text-white p-8">
          <h3 className="text-xl font-bold mb-6 flex items-center gap-2">
            <PieChart className="text-yellow-400" size={24} />
            기구별 예산 요약
          </h3>
          <div className="flex flex-col md:flex-row gap-6">
             <div className="flex-1 bg-gray-800/50 rounded-xl p-5 border border-gray-700 hover:bg-gray-800 transition-colors">
               <div className="flex justify-between items-start mb-2">
                 <p className="text-gray-400 text-sm">총동아리연합회</p>
                 <Users className="text-indigo-400 opacity-50" size={20} />
               </div>
               <p className="text-2xl font-bold mb-1">{formatCurrency(allianceTotal)}원</p>
               <div className="w-full bg-gray-700 h-1.5 rounded-full mt-2 overflow-hidden">
                 <div className="bg-indigo-500 h-full rounded-full" style={{ width: `${(allianceTotal / grandTotal) * 100}%` }}></div>
               </div>
               <p className="text-xs text-right text-gray-500 mt-1">{((allianceTotal / grandTotal) * 100).toFixed(1)}% 비중</p>
             </div>

             <div className="flex-1 bg-gray-800/50 rounded-xl p-5 border border-gray-700 hover:bg-gray-800 transition-colors">
               <div className="flex justify-between items-start mb-2">
                 <p className="text-gray-400 text-sm">총대의원회</p>
                 <Building className="text-emerald-400 opacity-50" size={20} />
               </div>
               <p className="text-2xl font-bold mb-1">{formatCurrency(councilTotal)}원</p>
               <div className="w-full bg-gray-700 h-1.5 rounded-full mt-2 overflow-hidden">
                 <div className="bg-emerald-500 h-full rounded-full" style={{ width: `${(councilTotal / grandTotal) * 100}%` }}></div>
               </div>
               <p className="text-xs text-right text-gray-500 mt-1">{((councilTotal / grandTotal) * 100).toFixed(1)}% 비중</p>
             </div>

             <div className="flex-1 bg-gradient-to-br from-indigo-900 to-slate-800 rounded-xl p-5 border border-indigo-700/50 shadow-lg relative overflow-hidden group">
               <div className="absolute top-0 right-0 w-24 h-24 bg-yellow-400/10 rounded-full blur-2xl group-hover:bg-yellow-400/20 transition-all"></div>
               <div className="relative z-10">
                  <p className="text-indigo-200 text-sm mb-1">전체 통합 예산</p>
                  <p className="text-3xl font-bold text-white mb-2">{formatCurrency(grandTotal)}원</p>
                  <div className="flex items-center gap-2 text-xs text-indigo-300">
                    <ArrowRight size={14} />
                    <span>2개 기구 합계</span>
                  </div>
               </div>
             </div>
          </div>
        </div>
      </div>
    </div>
  );
};

export default BudgetSheet;
