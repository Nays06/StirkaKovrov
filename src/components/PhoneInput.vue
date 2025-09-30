<template>
    <div class="phone-input">
        <div class="phone-input__wrapper">
            <div class="phone-input__country-select">
                <div class="phone-input__selected-country" @click="isCountryListOpen = !isCountryListOpen">
                    <span class="phone-input__flag">{{ selectedCountry.flag }}</span>
                    <span class="phone-input__code">+{{ selectedCountry.code }}</span>
                    <span class="phone-input__dropdown-arrow">▼</span>
                </div>

                <div v-if="isCountryListOpen" class="phone-input__country-list">
                    <div class="phone-input__search">
                        <input v-model="countrySearch" type="text" placeholder="Поиск страны..."
                            class="phone-input__search-input" @input="filterCountries">
                    </div>

                    <div class="phone-input__countries">
                        <div v-for="country in filteredCountries" :key="country.iso2" class="phone-input__country-item"
                            @click="selectCountry(country)">
                            <span class="phone-input__flag">{{ country.flag }}</span>
                            <span class="phone-input__country-name">{{ country.name }}</span>
                            <span class="phone-input__code">+{{ country.code }}</span>
                        </div>
                    </div>
                </div>
            </div>

            <input v-model="displayNumber" type="tel" :placeholder="placeholder" class="phone-input__number"
                :class="{ 'phone-input__number--error': !isValid }" @input="formatPhoneNumber"
                @blur="validatePhoneNumber" @keypress="onlyNumbers">
        </div>

        <div v-if="!isValid && errorMessage" class="phone-input__error">
            {{ errorMessage }}
        </div>
    </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue'

export default {
    name: 'PhoneInput',
    props: {
        modelValue: {
            type: String,
            default: ''
        },
        defaultCountry: {
            type: String,
            default: 'RU'
        }
    },
    emits: ['update:modelValue', 'validation'],

    setup(props, { emit }) {
        const displayNumber = ref('')
        const selectedCountry = ref({})
        const isCountryListOpen = ref(false)
        const countrySearch = ref('')
        const isValid = ref(true)
        const errorMessage = ref('')
        const allCountries = ref([])
        const filteredCountries = ref([])

        const countriesData = [
            { name: 'Россия', code: '7', iso2: 'RU', flag: '🇷🇺' },
            { name: 'США', code: '1', iso2: 'US', flag: '🇺🇸' },
            { name: 'Украина', code: '380', iso2: 'UA', flag: '🇺🇦' },
            { name: 'Казахстан', code: '7', iso2: 'KZ', flag: '🇰🇿' },
            { name: 'Беларусь', code: '375', iso2: 'BY', flag: '🇧🇾' },
            { name: 'Германия', code: '49', iso2: 'DE', flag: '🇩🇪' },
            { name: 'Франция', code: '33', iso2: 'FR', flag: '🇫🇷' },
            { name: 'Великобритания', code: '44', iso2: 'GB', flag: '🇬🇧' },
            { name: 'Китай', code: '86', iso2: 'CN', flag: '🇨🇳' },
            { name: 'Япония', code: '81', iso2: 'JP', flag: '🇯🇵' }
        ]

        const placeholder = computed(() => {
            if (!selectedCountry.value.code) return 'Введите номер телефона'

            const formats = {
                '7': '(000) 000-00-00',
                '1': '(000) 000-000',
                '380': '00 000 0000',
                '375': '00 000-00-00',
                '49': '000 0000000',
                '33': '0 00 00 00 00',
                '44': '0000 000000',
                '86': '000 0000 0000',
                '81': '00-0000-0000'
            }

            return formats[selectedCountry.value.code] || 'Введите номер телефона'
        })

        const formatPhoneNumber = (event) => {
            let input = event.target.value.replace(/\D/g, '')

            const maxLength = getMaxPhoneLength(selectedCountry.value.iso2)
            if (input.length > maxLength) {
                input = input.substring(0, maxLength)
            }

            let formatted = input
            switch (selectedCountry.value.iso2) {
                case 'RU':
                    if (input.length > 0) formatted = input
                    if (input.length > 3) formatted = `(${input.slice(0, 3)}) ${input.slice(3)}`
                    if (input.length > 6) formatted = `(${input.slice(0, 3)}) ${input.slice(3, 6)}-${input.slice(6)}`
                    if (input.length > 8) formatted = `(${input.slice(0, 3)}) ${input.slice(3, 6)}-${input.slice(6, 8)}-${input.slice(8)}`
                    break

                case 'US':
                    if (input.length > 0) formatted = input
                    if (input.length > 3) formatted = `(${input.slice(0, 3)}) ${input.slice(3)}`
                    if (input.length > 6) formatted = `(${input.slice(0, 3)}) ${input.slice(3, 6)}-${input.slice(6)}`
                    break

                case 'UA':
                    if (input.length > 0) formatted = input
                    if (input.length > 2) formatted = `${input.slice(0, 2)} ${input.slice(2)}`
                    if (input.length > 5) formatted = `${input.slice(0, 2)} ${input.slice(2, 5)} ${input.slice(5)}`
                    break

                case 'DE':
                    if (input.length > 0) formatted = input
                    if (input.length > 3) formatted = `${input.slice(0, 3)} ${input.slice(3)}`
                    break

                default:
                    if (input.length > 4) {
                        formatted = input.replace(/(\d{4})(?=\d)/g, '$1 ')
                    }
            }

            displayNumber.value = formatted
            validatePhoneNumber()
        }

        const onlyNumbers = (event) => {
            const charCode = event.which ? event.which : event.keyCode
            if (charCode > 31 && (charCode < 48 || charCode > 57)) {
                event.preventDefault()
            }
        }

        onMounted(() => {
            allCountries.value = countriesData
            filteredCountries.value = countriesData

            const defaultCountryData = countriesData.find(
                country => country.iso2 === props.defaultCountry
            ) || countriesData[0]

            selectCountry(defaultCountryData)

            if (props.modelValue) {
                const cleanNumber = props.modelValue.replace(/\D/g, '')
                displayNumber.value = cleanNumber
                formatPhoneNumber({ target: { value: cleanNumber } })
            }
        })

        const filterCountries = () => {
            if (!countrySearch.value.trim()) {
                filteredCountries.value = allCountries.value
                return
            }

            const searchTerm = countrySearch.value.toLowerCase()
            filteredCountries.value = allCountries.value.filter(country =>
                country.name.toLowerCase().includes(searchTerm) ||
                country.code.includes(searchTerm) ||
                country.iso2.toLowerCase().includes(searchTerm)
            )
        }

        const selectCountry = (country) => {
            selectedCountry.value = country
            isCountryListOpen.value = false
            countrySearch.value = ''
            filteredCountries.value = allCountries.value

            const cleanNumber = displayNumber.value.replace(/\D/g, '')
            formatPhoneNumber({ target: { value: cleanNumber } })
        }

        const validatePhoneNumber = () => {
            const cleanNumber = displayNumber.value.replace(/\D/g, '')

            if (!cleanNumber) {
                isValid.value = true
                errorMessage.value = ''
                emitValidation(cleanNumber)
                return
            }

            const minLength = getMinPhoneLength(selectedCountry.value.iso2)
            if (cleanNumber.length < minLength) {
                isValid.value = false
                errorMessage.value = `Номер слишком короткий. Минимум ${minLength} цифр`
                emitValidation(cleanNumber)
                return
            }

            const maxLength = getMaxPhoneLength(selectedCountry.value.iso2)
            if (cleanNumber.length > maxLength) {
                isValid.value = false
                errorMessage.value = `Номер слишком длинный. Максимум ${maxLength} цифр`
                emitValidation(cleanNumber)
                return
            }

            if (!isValidPhoneFormat(cleanNumber, selectedCountry.value.iso2)) {
                isValid.value = false
                errorMessage.value = 'Неверный формат номера'
                emitValidation(cleanNumber)
                return
            }

            isValid.value = true
            errorMessage.value = ''
            emitValidation(cleanNumber)
        }

        const getMinPhoneLength = (countryCode) => {
            const lengths = {
                'RU': 10,
                'US': 10,
                'UA': 9,
                'KZ': 10,
                'BY': 9,
                'DE': 10,
                'FR': 9,
                'GB': 10,
                'CN': 11,
                'JP': 10
            }
            return lengths[countryCode] || 8
        }

        const getMaxPhoneLength = (countryCode) => {
            const lengths = {
                'RU': 10,
                'US': 10,
                'UA': 9,
                'KZ': 10,
                'BY': 9,
                'DE': 11,
                'FR': 9,
                'GB': 10,
                'CN': 11,
                'JP': 11
            }
            return lengths[countryCode] || 15
        }

        const isValidPhoneFormat = (number, countryCode) => {
            const patterns = {
                'RU': /^[9]\d{9}$/,
                'US': /^\d{10}$/,
                'UA': /^\d{9}$/,
                'DE': /^\d{10,11}$/,
                'FR': /^\d{9}$/,
                'GB': /^\d{10}$/,
                'CN': /^\d{11}$/,
                'JP': /^\d{10,11}$/
            }

            const pattern = patterns[countryCode]
            return pattern ? pattern.test(number) : true
        }

        const emitValidation = (cleanNumber) => {
            const fullPhone = selectedCountry.value.code ?
                `+${selectedCountry.value.code}${cleanNumber}` :
                cleanNumber

            emit('update:modelValue', fullPhone)
            emit('validation', {
                isValid: isValid.value,
                phoneNumber: fullPhone,
                formattedNumber: displayNumber.value,
                country: selectedCountry.value
            })
        }

        const closeCountryList = (event) => {
            if (!event.target.closest('.phone-input__country-select')) {
                isCountryListOpen.value = false
            }
        }

        const getFormattedNumber = () => {
            return displayNumber.value
        }

        const getCleanNumber = () => {
            return displayNumber.value.replace(/\D/g, '')
        }

        const clear = () => {
            displayNumber.value = ''
            isValid.value = true
            errorMessage.value = ''
        }

        onMounted(() => {
            document.addEventListener('click', closeCountryList)
        })

        return {
            displayNumber,
            selectedCountry,
            isCountryListOpen,
            countrySearch,
            isValid,
            errorMessage,
            filteredCountries,
            placeholder,
            filterCountries,
            selectCountry,
            formatPhoneNumber,
            validatePhoneNumber,
            onlyNumbers,
            getFormattedNumber,
            getCleanNumber,
            clear
        }
    }
}
</script>

<style scoped>
.phone-input {
    font-family: Arial, sans-serif;
    position: relative;
    width: 100%;
    max-width: 460px;
}

.phone-input__wrapper {
    display: flex;
    align-items: center;
    border: 1px solid #ccc;
    border-radius: 4px;
    background: white;
    height: 56px;
    width: 100%;
    font-size: 16px;
}

.phone-input__country-select {
    position: relative;
    flex: 0 0 auto;
}

.phone-input__selected-country {
    display: flex;
    align-items: center;
    padding: 8px 0 8px 12px;
    cursor: pointer;
    height: 100%;
}

.phone-input__flag {
    margin-right: 8px;
    font-size: 16px;
}

.phone-input__code {
    font-weight: 500;
    margin-right: 8px;
}

.phone-input__dropdown-arrow {
    font-size: 10px;
    color: #666;
    margin-right: 8px;
}

.phone-input__country-list {
    position: absolute;
    top: 100%;
    left: 0;
    width: 278px;
    background: white;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    z-index: 10000;
    overflow-y: hidden;
    margin-top: 2px;
}

.phone-input__search {
    padding: 8px;
    border-bottom: 1px solid #eee;
    position: sticky;
    top: 0;
    background: white;
    z-index: 10001;
}

.phone-input__search-input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    outline: none;
    font-size: 14px;
}

.phone-input__countries {
    max-height: 250px;
    overflow-y: scroll;
}

.phone-input__country-item {
    display: flex;
    align-items: center;
    padding: 8px 12px;
    cursor: pointer;
    border-bottom: 1px solid #f0f0f0;
}

.phone-input__country-item:hover {
    background: #f0f0f0;
}

.phone-input__country-name {
    flex: 1;
    margin: 0 8px;
    font-size: 14px;
}

.phone-input__code {
    font-size: 14px;
}

.phone-input__number {
    flex: 1;
    padding: 8px 12px;
    border: none;
    outline: none;
    font-size: 16px;
    height: 100%;
}

.phone-input__number--error {
    border-color: #ff4444;
}

.phone-input__error {
    color: #ff4444;
    font-size: 12px;
    margin-top: 4px;
    position: relative;
    z-index: 2;
}

@media (max-width: 1200px) {
    .phone-input {
        max-width: 400px;
    }

    .phone-input__wrapper {
        height: 50px;
        font-size: 15px;
    }

    .phone-input__country-list {
        width: 280px;
    }

    .phone-input__selected-country {
        padding: 6px 0 6px 10px;
    }

    .phone-input__flag {
        font-size: 15px;
        margin-right: 6px;
    }

    .phone-input__code {
        font-size: 15px;
        margin-right: 6px;
    }

    .phone-input__dropdown-arrow {
        font-size: 9px;
        margin-right: 6px;
    }

    .phone-input__number {
        font-size: 15px;
        padding: 6px 10px;
    }

    .phone-input__error {
        font-size: 11px;
    }
}

@media (max-width: 768px) {
    .phone-input {
        max-width: 100%;
    }

    .phone-input__wrapper {
        height: 48px;
        font-size: 14px;
    }

    .phone-input__country-list {
        width: auto;
        left: 0;
        max-height: 250px;
        overflow: scroll;
    }

    .phone-input__search-input {
        font-size: 13px;
        padding: 6px;
    }

    .phone-input__country-item {
        padding: 6px 10px;
    }

    .phone-input__country-name,
    .phone-input__code {
        font-size: 13px;
    }

    .phone-input__selected-country {
        padding: 6px 0 6px 8px;
    }

    .phone-input__flag {
        font-size: 14px;
        margin-right: 5px;
    }

    .phone-input__code {
        font-size: 14px;
        margin-right: 5px;
    }

    .phone-input__dropdown-arrow {
        font-size: 8px;
        margin-right: 5px;
    }

    .phone-input__number {
        font-size: 14px;
        padding: 6px 8px;
    }

    .phone-input__error {
        font-size: 10px;
        margin-top: 3px;
    }
}

@media (max-width: 480px) {
    .phone-input__wrapper {
        height: 44px;
        font-size: 13px;
    }

    .phone-input__country-list {
        max-height: 200px;
    }

    .phone-input__search {
        padding: 6px;
    }

    .phone-input__search-input {
        font-size: 12px;
        padding: 5px;
    }

    .phone-input__countries {
        overflow-y: visible;
    }

    .phone-input__country-item {
        padding: 5px 8px;
    }

    .phone-input__country-name,
    .phone-input__code {
        font-size: 12px;
        margin: 0 6px;
    }

    .phone-input__selected-country {
        padding: 5px 0 5px 6px;
    }

    .phone-input__flag {
        font-size: 13px;
        margin-right: 4px;
    }

    .phone-input__code {
        font-size: 13px;
        margin-right: 4px;
    }

    .phone-input__dropdown-arrow {
        font-size: 7px;
        margin-right: 4px;
    }

    .phone-input__number {
        font-size: 13px;
        padding: 5px 6px;
    }

    .phone-input__error {
        font-size: 9px;
        margin-top: 2px;
    }
}

@media (max-width: 360px) {
    .phone-input__wrapper {
        height: 40px;
        font-size: 12px;
    }

    .phone-input__country-list {
        max-height: 180px;
    }

    .phone-input__search {
        padding: 5px;
    }

    .phone-input__search-input {
        font-size: 11px;
        padding: 4px;
    }

    .phone-input__country-item {
        padding: 4px 6px;
    }

    .phone-input__country-name,
    .phone-input__code {
        font-size: 11px;
        margin: 0 5px;
    }

    .phone-input__selected-country {
        padding: 4px 0 4px 5px;
    }

    .phone-input__flag {
        font-size: 12px;
        margin-right: 3px;
    }

    .phone-input__code {
        font-size: 12px;
        margin-right: 3px;
    }

    .phone-input__dropdown-arrow {
        font-size: 6px;
        margin-right: 3px;
    }

    .phone-input__number {
        font-size: 12px;
        padding: 4px 5px;
    }

    .phone-input__error {
        font-size: 8px;
        margin-top: 2px;
    }
}
</style>