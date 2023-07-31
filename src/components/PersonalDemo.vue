
<template>
    <div class="stepsdemo-content">
        <Card>
            <template v-slot:title>
                Instrumentos
            </template>
            <template v-slot:content>
                <div class="formgrid grid">
                    <div class="field col-5">
                        <div class="field">
                            <label>Tipo de Calibração</label>
                            <Dropdown v-model="tipoCalibracao" :options="listaTipoCalibracao" optionLabel="name" placeholder="Tipo de Calibração" class="text-base text-color surface-overlay border-1 border-solid surface-border border-round appearance-none outline-none focus:border-primary w-full" />
                        </div>
                    </div>                    
                    <div class="field col-5">
                        <label>Local de Execução</label>
                        <Dropdown v-model="localExecucao" :options="listaLocalExecucao" optionLabel="name" placeholder="Local de Execução" class="text-base text-color surface-overlay border-1 border-solid surface-border border-round appearance-none outline-none focus:border-primary w-full" />
                    </div>                
                    <div class="field col-2">
                        <label>Prazo de Entrega</label>
                        <InputText v-model="prazoEntrega" class="text-base text-color surface-overlay border-1 border-solid surface-border border-round appearance-none outline-none focus:border-primary w-full"/>
                    </div>
                    <div class="fiel col">
                        <DataTable v-model:filters="filters" v-model:selection="instrumentosSelecionados" :value="instrumentos" dataKey="codigo" tableStyle="min-width: 50rem" :loading="loading" :globalFilterFields="['codigo', 'tipoInstrumento', 'modeloInstrumento']">
                        <template #header>
                            <div class="flex justify-content-end">
                                <span class="p-input-icon-left">
                                    <i class="pi pi-search" />
                                    <InputText v-model="filters['global'].value" placeholder="Pesquisar..." />
                                </span>
                            </div>
                        </template>
                        <Column selectionMode="multiple" headerStyle="width: 3rem"></Column>
                        <Column field="codigo" header="Código"></Column>
                        <Column field="tipoInstrumento" header="Tipo Instrumento"></Column>
                        <Column field="modeloInstrumento" header="Modelo Instrumento"></Column>
                        </DataTable>                    
                    </div>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <i></i>
                    <Button label="Próximo" @click="nextPage()" icon="pi pi-angle-right" iconPos="right" />
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
import { FilterMatchMode } from 'primevue/api';

export default {
    data () {
        return {
            firstname: '',
            lastname: '',
            age: null,
            tipoCalibracao: null,
            localExecucao: null,
            prazoEntrega: 10,
            submitted: false,
            validationErrors: {},
            listaTipoCalibracao: [
                { name: 'Rastreado', code: 'Rastreado' },
                { name: 'RBL', code: 'RBL' },
                { name: 'RBLE', code: 'RBLE' }
            ],
            listaLocalExecucao: [
                { name: 'Campo', code: 'Campo' },
                { name: 'Laboratório', code: 'Laboratório' }
            ],
            instrumentos: [
                { codigo: '0001', tipoInstrumento: 'Paquimetro', modeloInstrumento: 'Paquimetro XPTO' },
                { codigo: '0002', tipoInstrumento: 'Calibrador de Boca', modeloInstrumento: 'Calibrador de Boca XPTO' },
                { codigo: '0003', tipoInstrumento: 'Relógio Comparador', modeloInstrumento: 'Relógio Comparador XPTO' },
            ],
            instrumentosSelecionados: [],
            filters: {
                global: { value: null, matchMode: FilterMatchMode.CONTAINS },
            }
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page', {pageIndex: 0});
        }
    }
}
</script>
